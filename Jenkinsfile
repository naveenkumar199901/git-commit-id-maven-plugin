pipeline {
  agent any
  parameters {
 	booleanParam (
	  defaultValue: false,
	  description: 'Upload this version to repository?',
	  name : 'https://github.com/kharchessk/Test-Repo.git')
  	  
  }
  
  stages {
        
	stage('Deploy to repository') {
	  when {
		expression {
			  return params.UPLOAD_TO_REPOSITORY
		  }
	  }
	  steps {
		echo 'Updating version before uploading to repository...'

		sh 'mvn build-helper:parse-version versions:set -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.incrementalVersion}-BUILD-${BUILD_NUMBER} versions:commit'
		echo 'Deploying to respository...'
		sh 'mvn -DskipTests clean deploy'
		echo 'Tagging version'
		sh 'mvn -Dusername="jenkins" scm:tag'
	  }
	}

  }
}
