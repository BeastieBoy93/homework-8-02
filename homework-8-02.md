# Домашнее задание к занятию "`Что такое DevOps. СI/СD`" - `Эсадов Роман`
---
### Задание 1
`Git`

![Git](https://github.com/BeastieBoy93/homework-8-02/blob/main/1.png)

`Build steps`

![Build Steps](https://github.com/BeastieBoy93/homework-8-02/blob/main/2.png)

`Result`

![Result](https://github.com/BeastieBoy93/homework-8-02/blob/main/3.png)

---

### Задание 2
`Pipeline script`
```
pipeline {
 agent any
 stages {
  stage('Git') {
   steps {git 'https://github.com/BeastieBoy93/homework-8-02.git'}
  }
  stage('Test') {
   steps {
    sh '/usr/local/go/bin/go test .'
   }
  }
  stage('Build') {
   steps {
    sh 'docker build .'
   }
  }
 }
}
```
`Result`

![Result](https://github.com/BeastieBoy93/homework-8-02/blob/main/4.png)

---

### Задание 3
`Pipeline script`
```
pipeline {
 agent any
 stages {
  stage('Git') {
   steps {git 'https://github.com/BeastieBoy93/homework-8-02.git'}
  }
  stage('Test') {
   steps {
    sh '/usr/local/go/bin/go test .'
   }
  }
  stage('Build') {
   steps {
    sh 'CGO_ENABLED=0 GOOS=linux /usr/local/go/bin/go build -a -installsuffix nocgo -o /home/jenkins/app .'
   }
  }
  stage('Push') {
   steps {
    sh 'curl -u "admin:admin" --upload-file "/home/jenkins/app" "http://158.160.44.203:8081/repository/my_repo/app"'
   }
  }
 }
}
```
`Result 1`

![Result 1](https://github.com/BeastieBoy93/homework-8-02/blob/main/5.png)

`Result 2`

![Result 2](https://github.com/BeastieBoy93/homework-8-02/blob/main/6.png)
