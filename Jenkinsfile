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
                    python3 -m venv /tmp/.env
                    . /tmp/.env/bin/activate
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
                    . /tmp/.env/bin/activate
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
                    . /tmp/.env/bin/activate
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
                    . /tmp/.env/bin/activate
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
