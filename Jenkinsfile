#!groovy
build('java-shared-resources', 'docker-host') {
    checkoutRepo()
    loadBuildUtils()

    def javaLibPipeline
    runStage('load JavaLib pipeline') {
        javaLibPipeline = load("build_utils/jenkins_lib/pipeJavaLib.groovy")
    }

    def buildImageTag = "80c38dc638c0879687f6661f4e16e8de9fc0d2c6"
    javaLibPipeline(buildImageTag)
}