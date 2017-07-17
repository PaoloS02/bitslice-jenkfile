
node ('atlasnode') {
  // Cleanup previous runs
  stage('Cleanup') {
    deleteDir()
  } // end Cleanup

  // Checkout git repositories
  stage('Checkout') {
  	dir('llvm') {
      git url: 'https://github.com/PaoloS02/llvm-bitslicer.git', branch: 'master'
    }
    
    dir('clang') {
      git url: 'https://github.com/PaoloS02/clang-bitslicer.git', branch: 'master'
    }
  
  }
  
   stage('Build') {
    docker.image('embecosm/builder:ubuntu-16.04').inside {
      sh script: '''THREADS=`cat /proc/cpuinfo | grep -c processor`
      mkdir build && cd build && cmake -DCMAKE_BUILD_TYPE=Debug -DLLVM_ENABLE_ASSERTIONS=ON -DBUILD_SHARED_LIBS=ON  ../llvm && make -j $THREADS'''
      
    }
 }
