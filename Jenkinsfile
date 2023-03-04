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
		echo "build bento and containerize it"
		script {
		    sh """
                    . .env/bin/activate
                    bentoml build && bentoml containerize iris_classifier:latest
                    """
		}
	    }
	}
    }
}
