/* groovylint-disable-next-line CompileStatic */
pipeline {
    
    agent any
    stages {
        stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

            app = docker.build("kiyatilahun/OctaneTest")
        }
    }
}
