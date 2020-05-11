# Part2 Reachability Analysis
## Input Uncertainty
* Method1: Analytical
* Method2: Gazebo experiemental
* Method3: real-experiemental (also as validition for other methods)
* Method_New1: sensor measurement error + detection algorithm err from gazebo (simulate perfect sensor in gazebo)
* [To merge 2 gaussian distribution](https://math.stackexchange.com/questions/453113/how-to-merge-two-gaussians)

* Method1 (not feasible)
    * Sensor measurement error:
        * Kinect 
        Depth resolution: ~ 1.5 mm at 50 cm. About 5 cm at 5 m
        Noise: About +-1 DN at all depths. This means +-1 mm close, and +- 5 cm far.

        * Ouster OS-1 16-Zeilen
        RANGE: 120 m
        PRECISION: ±1.5 – 10 cm

    * Error from detectors (e.g. leg_detecot/ upper_body_detecor)
        * Purpose1: detector algorithm itself does not generate localization error? since it's only doing recognition
            * to verify: In gazebo with single detector and perfect sensor

    * Error from sensor-fusion
        * Sensor fusion matches detection from 2 detectors
        * when matched take mean-pose as new fused_pose
        * Covariance is set to mean of 2 covariances too. (Not how it supposed to be)

* Method2, details of experiment setup
In gazebo sensor are simulated as perfect (No noise)
    1. Single detector (leg/upper)
        a. static single person to get static localisation err [3*3 locations]
        b. Single moving person [Normal] 
        c. Single moving person [Slow]
        d. Single moving person [fast]
        e. multiple people
    Visulise results if its plausible [Idealwise pose should be perfect]
    2. Tracker [fused]
        b. Single moving person [Normal] 
        c. Single moving person [Slow]
        d. Single moving person [fast]
        e. multiple people

* Detector's uncertainty
    * Leg_detecot (DavidLu)
        * with real-time covariance, pos.covariance[0] = pow(0.3 / reliability, 2.0); ideal case cov = 0.09
        * If this is a experience-formel, has to be validated through tests

* To Systematically analysis and summerize the uncertainty from gazebo-experient

    * A python script is written to record the data
        1. For single person, easy
        2. For multiple person, a match method is needed -> Benchmark provide help

    * Valid sensor range is essential for us
        * In frame: robot base
            * RGB-D: 
                * depth 2.2 ~ 6.4 # Change plugin parameter of point cloud cut off 0.5 ~5 
                * horizotal range +- 0.3 at 2.2, +-2,7 at 6.4 
            * Laser: 
                * depth 2 ~ 6,7
                * horizotal: +- 0.3 at 2, +-4 at 6, +-2.4 at 6.7
            * Laser high recall:
                * depth 2 ~ 15
                * horizotal: +-2 at 2, +-8 at 10 [almost the whole laser range]
            



    * Some comment to the citaion in seminar-report

    [45]: Meanly focused on the robustness of the Collision-waring system against the sensor err

