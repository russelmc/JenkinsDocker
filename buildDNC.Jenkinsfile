def dockerImage;

node('docker'){
	stage('SCM'){
		checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/russelmc/JenkinsDocker']]]);
	}
	stage('build'){
		dockerImage = docker.build('russelmcg/agent-dnc:v' + env.BUILD_NUMBER, './dotnetcore');
	}
	stage('push'){
		docker.withRegistry('https://index.docker.io/v1/', 'dockerhubcreds'){
			dockerImage.push();
		}

		// docker.withRegistry('', 'dockerhubcreds'){
		// 	dockerImage.push();
		// }
	}
}