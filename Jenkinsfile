pipeline {
    agent any

    stages {
	stage("Checkout") {
	    steps {
		echo "checkout"
	    }
	}
	stage("Install Depdendencies") {
	    steps {
		echo "install dependencies"
		script {
		    sh """
                    python3 -m venv .env
                    . .env/bin/activate
                    pip install -U pip
                    pip install -Ur requirements.txt
                    """
		}
	    }
	}
	stage("Train") {
	    steps {
		echo "train model"
		script {
		    sh """
                    . .env/bin/activate
                    python3 train.py
                    """
		}
	    }
	}
	stage("Build") {
	    steps {
		echo "build bento"
		script {
		    sh """
                    . .env/bin/activate
                    bentoml build
                    """
		}
	    }
	}
	stage("Containerize") {
	    steps {
		echo "containerize the bento"
		script {
		    sh """
                    . .env/bin/activate
                    bentoml containerize iris_classifier:latest
                    """
		}
	    }
	}
	stage("Push") {
	    steps {
		echo "push the docker image to registry"
	    }
	}
    }
}
