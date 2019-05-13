stage 'CI'
node {

    checkout scm

    //git branch: 'jenkins2-course', 
<<<<<<< HEAD
        //url: 'https://github.com/hong-zhou/solitaire-systemjs-course.git'

    // pull dependencies from npm
    // on windows use: bat 'npm install'
    // sh 'npm install'
	
	bat 'npm install'

=======
    //    url: 'https://github.com/g0t4/solitaire-systemjs-course'

    // pull dependencies from npm
    // on windows use: 
    //sh 'npm install'
    bat 'npm install'
>>>>>>> a6ad1e2917ba1eb4e8440349a7b218c10c1fc72b
    // stash code & dependencies to expedite subsequent testing
    // and ensure same code & dependencies are used throughout the pipeline
    // stash is a temporary archive
    stash name: 'everything', 
          excludes: 'test-results/**', 
          includes: '**'
    
    // test with PhantomJS for "fast" "generic" results
<<<<<<< HEAD
    // on windows use: bat 'npm run test-single-run -- --browsers PhantomJS'
    //sh 'npm run test-single-run -- --browsers PhantomJS'
	
	bat 'npm run test-single-run -- --browsers PhantomJS'
    
=======
    // on windows use: 
    // sh 'npm run test-single-run -- --browsers PhantomJS'
    bat 'npm run test-single-run -- --browsers Edge'
>>>>>>> a6ad1e2917ba1eb4e8440349a7b218c10c1fc72b
    // archive karma test results (karma is configured to export junit xml files)
    step([$class: 'JUnitResultArchiver', 
          testResults: 'test-results/**/test-results.xml'])
          
}

// demoing a second agent
node {
    // on windows use: bat 'dir'
    // sh 'ls'
<<<<<<< HEAD
	
	bat 'dir'

    // on windows use: bat 'del /S /Q *'
    // sh 'rm -rf *'
	
	bat 'del /S /Q *'

    unstash 'everything'

    // on windows use: bat 'dir'
    //sh 'ls'
	
	bat 'dir'
=======
    bat 'dir'
    // on windows use: bat 'del /S /Q *'
    // sh 'rm -rf *'
bat 'del /S /Q *'
    unstash 'everything'

    // on windows use: bat 'dir'
    // sh 'ls'
    bat 'dir'
>>>>>>> a6ad1e2917ba1eb4e8440349a7b218c10c1fc72b
}

//parallel integration testing
stage 'Browser Testing'
parallel chrome: {
    runTests("Chrome")
}, edge: {
    runTests("Edge")
}

def runTests(browser) {
    node {
        // on windows use: bat 'del /S /Q *'
        // sh 'rm -rf *'
<<<<<<< HEAD
		
		bat 'del /S /Q *'

        unstash 'everything'

        // on windows use: bat "npm run test-single-run -- --browsers ${browser}"
        // sh "npm run test-single-run -- --browsers ${browser}"
		bat "npm run test-single-run -- --browsers ${browser}"

=======
bat 'del /S /Q *'
        unstash 'everything'

        // on windows use: bat "npm run test-single-run -- --browsers ${browser}"
        //sh "npm run test-single-run -- --browsers ${browser}"
bat "npm run test-single-run -- --browsers ${browser}"
>>>>>>> a6ad1e2917ba1eb4e8440349a7b218c10c1fc72b
        step([$class: 'JUnitResultArchiver', 
              testResults: 'test-results/**/test-results.xml'])
    }
}

node {
    notify("Deploy to staging?")
}

input 'Deploy to staging?'

// limit concurrency so we don't perform simultaneous deploys
// and if multiple pipelines are executing, 
// newest is only that will be allowed through, rest will be canceled
stage name: 'Deploy to staging', concurrency: 1
node {
    // write build number to index page so we can see this update
    // on windows use: bat "echo '<h1>${env.BUILD_DISPLAY_NAME}</h1>' >> app/index.html"
<<<<<<< HEAD
    // sh "echo '<h1>${env.BUILD_DISPLAY_NAME}</h1>' >> app/index.html"
    bat "echo '<h1>${env.BUILD_DISPLAY_NAME}</h1>' >> app/index.html"
	
    // deploy to a docker container mapped to port 3000
    // on windows use: bat 'docker-compose up -d --build'
    // sh 'docker-compose up -d --build'
    bat 'docker-compose up -d --build'
	
=======
    //sh "echo '<h1>${env.BUILD_DISPLAY_NAME}</h1>' >> app/index.html"
    bat "echo '<h1>${env.BUILD_DISPLAY_NAME}</h1>' >> app/index.html"
    // deploy to a docker container mapped to port 3000
    // on windows use: bat 'docker-compose up -d --build'
    //sh 'docker-compose up -d --build'
    bat 'docker-compose up -d --build'
>>>>>>> a6ad1e2917ba1eb4e8440349a7b218c10c1fc72b
    notify 'Solitaire Deployed!'
}











def notify(status){
    emailext (
      to: "zhsnnu@gmail.com",
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}
