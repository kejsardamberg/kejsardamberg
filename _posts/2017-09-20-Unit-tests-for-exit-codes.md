# Creating unit tests for exit codes other than 0 (success)

The testing framework has implemented exit code table to be able to easily integrate with Jenkins, TeamCity and other build engines. Writing unit tests for the exit codes initially proved hard since executing anything that ended with anything other than 0 stopped the JVM execution, thus preventing any asserts. Hence we implemented a test mode for the framework. If a variable called testMode is set to true, a system property is set to the exit code - thus being able to assert. 

To be able to execute tests of the behavior of the testing framework used from the command line interface we had to implement

        if(!testMode) {
            System.exit(TestRun.exitCode);
        } else {
            System.setProperty("TAF latest test run exit code", String.valueOf(TestRun.exitCode));
        }

One word of warning, from experience. Don't forget to reset your exit code (probably even in a @Before method of your test class) before the next test case. 
