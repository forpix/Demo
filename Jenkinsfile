pipeline {
    agent any
    stages {
        stage("Package on Tem.Branch") {
            steps {
                sh '''
		    pwd
		    git remote update
		    git checkout origin/Tempo
		    git fetch 
		    git pull --rebase origin Tempo
		    ls -a
		    git branch 
		    '''
}
		post {
			success {
			    sh '''
			git checkout Stage_1
			git pull origin Tempo
			git merge Tempo
			git pull --rebase origin
			git remote set-url origin http://forpix:mdali%40786@github.com/forpix/Demo.git
			git push -u origin Stage_1
			'''
				}
			failure {
			    sh '''
			   git remote set-url origin http://forpix:mdali%40786@github.com/forpix/Demo.git
			   git push origin origin --delete Tempo 
			   git branch -d Tempo 
			   '''
						}
					}
    }
	stage("Stage_1 Branch") {
            steps {
                sh '''
		git checkout Stage_1
		git branch
		ls 
		'''
		}
		post {
			success {
			    sh '''
			git checkout Stage_2
			git pull origin Stage_2
			git merge Stage_1
			git remote set-url origin http://forpix:mdali%40786@github.com/forpix/Demo.git
			git push -u origin Stage_2
			'''
				}
			failure {
			   echo "The build failed at Stage_1 Branch"
						}
					}
    }
	stage("Stage_2 Branch") {
            steps {
                sh '''
		git checkout Stage_2
		git branch
		ls 
		'''
		}
		post {
			success {
			    sh '''
			git checkout Stage_3
			git pull origin Stage_3
			git merge Stage_2
			git remote set-url origin http://forpix:mdali%40786@github.com/forpix/Demo.git
			git push -u origin Stage_3
			'''
				}
			failure {
			   echo "The build failed at Stage_2 Branch"
						}
					}
    }
	stage("Stage_3 Branch") {
            steps {
                sh '''
		git checkout Stage_3
		git branch
		ls 
		'''
		}
		post {
			success {
			sh '''
			git checkout Delivery
			git pull origin Delivery
			git merge Stage_3
			git remote set-url origin http://forpix:mdali%40786@github.com/forpix/Demo.git
			git push -u origin Delivery
			'''
				}
			failure {
			   echo "The build failed at Stage_3 Branch"
						}
					}
    }
    }
    post { 
        success{ 
               echo 'build is successful'
        }   
        }
        
}
