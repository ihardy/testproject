pipeline {
    agent { docker { image 'node:8-alpine' } }

    environment {
        TEST_VAR = 'a_test_env_var'
    }

    stages {
        stage('steps') {
          sh 'yarn install'
          def yarnLock = new File('yarn.lock')
          def lines = yarnLock.readLines()
          def stripesPkgs = []
        
          //parse yarn.lock for matches to @folio/stripes-*
          for (line in lines) {
            if (line =~ /^"(@folio\/stripes-.*@).*\d":$/) {
              def matcher = (line =~ /^"(@folio\/stripes-.*)@.*\d":$/)
              stripesPkgs.add(matcher[0][1])
            }
          }
          def duplicates = false //initialize default condition
          // check for duplicates
          stripesPkgs.sort()
          def count = 1 
          while (count < stripesPkgs.size()) {
            if (stripesPkgs[count] == stripesPkgs[count -1]) {
              println stripesPkgs[count] + " is a duplicate"
              sh "yarn why ${stripesPkgs[count]}"
              duplicates = true
            }
            count += 1
          }
        
          if (duplicates == true) {
            echo "dupes found"
          } else {
            echo "No stripes-* duplicates found in yarn.lock"
          }
      } // end stage
    }
}

