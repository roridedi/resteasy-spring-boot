#!/usr/bin/groovy

/**
 this section of the pipeline executes on the master, which has a lot of useful variables that we can leverage to configure our pipeline
 **/
node('') {
    // these should align to the projects in the Application Inventory
    env.NAMESPACE = env.OPENSHIFT_BUILD_NAMESPACE.reverse().drop(6).reverse()
    env.QA_PROJECT = "${env.NAMESPACE}-qa"
    env.RELEASE_PROJECT = "${env.NAMESPACE}-et"

    // this value should be set to the root directory of your source code within the git repository.
    // if the root of the source is the root of the repo, leave this value as ""
    env.SOURCE_CONTEXT_DIR = ""
    env.APP_NAME = "${env.JOB_NAME}".replaceAll(/-?${env.PROJECT_NAME}-?/, '').replaceAll(/-?pipeline-?/, '')

    // these are defaults that will help run openshift automation
    env.OCP_API_SERVER = "${env.OPENSHIFT_API_URL}"
    env.OCP_TOKEN = readFile('/var/run/secrets/kubernetes.io/serviceaccount/token').trim()

    echo 'namespace: ' + env.NAMESPACE
    echo 'app name: ' + env.APP_NAME
    echo 'job name: ' + env.JOB_NAME
    echo 'project name: ' + env.PROJECT_NAME
    echo 'openshift build namespace: ' + env.OPENSHIFT_BUILD_NAMESPACE
}

//using the base slave image because we don't need anything else like maven or npm
node('jenkins-slave-base-rhel7'){

    stage('Scale Down Blue Deployment') {

    if (openshift.selector("dc",env.NAMESPACE).exists()) {
              openshift.selector("dc", env.NAMESPACE).delete()
            }



        // check deployment completed
      //  openshiftVerifyDeployment(apiURL: "${env.OCP_API_SERVER}", authToken: "${env.OCP_TOKEN}", depCfg: "${env.APP_NAME}", namespace: "${env.QA_PROJECT}", verifyReplicaCount: true)
    }

    stage('Notify QA'){
        notify("DEPLOYED TO ${env.QA_PROJECT}" as String)
    }

    timeout(time:15, unit:'MINUTES'){
        input "Begin Automated Testing Phase?"
    }

    //put automated testing here

    timeout(time:15, unit:'MINUTES'){
        input "Approve for Release?"
    }

    stage('Notify for Release'){
        notify("${env.QA_PROJECT} ready to be released" as String)
    }

}
