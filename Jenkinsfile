pipeline {
    agent any
    stages {
        stage('Install Node') {  
            agent {
                docker { image 'node' }
            } 
            steps('Install newman newman-reporter-htmlextra') {
                sh 'node -v'
                sh 'npm -v'
                sh 'pwd'
                sh 'ls'
                sh 'npm config set registry https://registry.npmmirror.com/'
                sh 'npm i newman '
                sh 'npm i newman-reporter-htmlextra'
                sh 'npx newman --version'
                sh 'npx newman-reporter-htmlextra --version'
                sh 'pwd'
                sh 'ls'
                sh 'rm -rf newman/*'
                sh  '''
                    npx newman run collection-1020.postman_collection.json -e 1020-dev.postman_environment.json -r htmlextra || true
                    '''
            }
        }  
    }
    post {
        success{
            mail to: 'he529564582@163.com',
                subject: "构建成功: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                        <!DOCTYPE html>
                        <html>
                            <head>
                                <meta charset="UTF-8">
                                <title>构建成功 - ${env.JOB_NAME} #${env.BUILD_NUMBER}</title>
                            </head>
                            <body>
                                <table width="95%" cellpadding="0" cellspacing="0"  style="font-size: 11pt; font-family: Tahoma, Arial, Helvetica, sans-serif">    
                                    <tr>    
                                        本邮件由系统自动发出，无需回复！<br/>            
                                        大家好，以下为 ${env.JOB_NAME } 项目构建信息</br> 
                                        <td><font color="#CC0000">构建结果 - ${currentBuild.result}</font></td>   
                                    </tr>    
                                    <tr>    
                                        <td><br />    
                                        <b><font color="#0B610B">构建信息</font></b>    
                                        <hr size="2" width="100%" align="center" /></td>    
                                    </tr>    
                                    <tr>    
                                        <td>    
                                            <ul>    
                                                <li>项目名称: ${env.JOB_NAME}</li>    
                                                <li>构建编号: 第 ${BUILD_NUMBER} 次构建</li>            
                                                <li>构建URL: <a href="${BUILD_URL}">${BUILD_URL}</a></li>
                                                <li>构建日志:<a href="${BUILD_URL}console">${BUILD_URL}console</a></li>
                                                <li>最近提交: <a href="${BUILD_URL}changes">${BUILD_URL}changes</a</li> 
                                                <li>测试报告: <a href="${env.BUILD_URL}Newman_20Report">${env.BUILD_URL}Newman_Report</a></li>  
                                            </ul>    
                                        </td>    
                                    </tr>    
                                </table>  
                            </body>
                        </html>
                        """,
                mimeType: 'text/html'
        }
        
        failure {
            mail to: 'he529564582@163.com',
                subject: "构建失败: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body:"""
                        <!DOCTYPE html>
                        <html>
                            <head>
                                <meta charset="UTF-8">
                                <title>构建失败 - ${env.JOB_NAME} #${env.BUILD_NUMBER}</title>
                            </head>
                            <body>
                                <table width="95%" cellpadding="0" cellspacing="0"  style="font-size: 11pt; font-family: Tahoma, Arial, Helvetica, sans-serif">    
                                    <tr>    
                                        本邮件由系统自动发出，无需回复！<br/>            
                                        大家好，以下为 ${env.JOB_NAME } 项目构建信息</br> 
                                        <td><font color="#CC0000">构建结果 -  ${currentBuild.result}</font></td> 
                                    </tr>    
                                    <tr>    
                                        <td><br />    
                                        <b><font color="#B40404">构建信息</font></b>    
                                        <hr size="2" width="100%" align="center" /></td>    
                                    </tr>    
                                    <tr>    
                                        <td>    
                                            <ul>    
                                                <li>项目名称: ${env.JOB_NAME}</li>    
                                                <li>构建编号: 第 ${env.BUILD_NUMBER} 次构建</li>            
                                                <li>构建URL: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></li>
                                                <li>构建日志： <a href="${env.BUILD_URL}console">${env.BUILD_URL}console</a></li>
                                                <li>最近提交: <a href="${env.BUILD_URL}changes">${env.BUILD_URL}changes</a></li>  
                                            </ul>    
                                        </td>    
                                    </tr>    
                                </table>  
                            </body>
                        </html>
                    """,
                mimeType: 'text/html'
        }
        // always {
        //     // Archive the HTML report
        //     archiveArtifacts artifacts: 'newman/*.html', allowEmptyArchive: false
        // }
        always {
            // Publish the HTML report using HTML Publisher
            publishHTML(target: [
                reportName: 'Newman Report', 
                reportDir: 'newman',       // Directory containing the report
                reportFiles: 'Collection1020-*.html', // HTML file pattern
                keepAll: true,             // Keep past reports
                allowMissing: false,       // Fail the build if report is missing
                alwaysLinkToLastBuild: true
            ])
        }
    }
}
