pipeline
{
agent none
stages
{
 stage('Non-parallel stage ')
 {
 agent {label "master"}
 steps { git 'https://github.com/sinarvek/PipeLineProject.git' }
 }
 stage('Build')
 {
 agent {label "master"}
 steps {bat 'Stage1.bat' }
 }
 stage('Run in parallel')
 {
 parallel
 {
 stage('Test1 on master')
 {
 agent {label "master"}
 steps {bat'Stage2.bat' }
 }
 stage('Test2 on slave machine')
 {
 agent {label "WS"}
 steps {bat'Stage3.bat' }
 }
 }
 }
 stage('Deploy')
 {
 agent {label "master"}
 steps {bat'Stage3.bat'}
 }
}

post
{
always{ echo "this will always run"}
success{ echo "this will run if all steps run successfully"}
failure{echo "this will run only when one step fail"}
unstable{echo "this will run only if the run marked as unstable"}
changed{echo "this will run only if the state of the pipeline changed , example the pipeline was previously failure and now is success"}
}
}
