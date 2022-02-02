# Full Open Source Blinky on XC7KL325T using yosys+nextpnr-xilinx

![image](https://user-images.githubusercontent.com/148607/152079663-e42ce6ed-66ef-461e-aed7-82a4e5667e39.png)
https://user-images.githubusercontent.com/148607/152079511-89539119-5d66-42f2-a709-3e35a81d7c0f.mp4

# Status
* works on the QMTech XC7K325T board
* does not build yet on Digilent Genesys2

# How to reproduce
1. clone and install yosys
2. git clone 
3. git clone https://github.com/kintex-chatter/nextpnr-xilinx.git
4. cd nextpnr-xilinx
5. git checkout xilinx-upstream
6. mkdir build
7. pushd build
8. cmake -DARCH=xilinx ..
9. make && sudo make install
10. popd
11. pushd xilinx/external
12. rm -rf prjxray-db
13. git clone https://github.com/kintex-chatter/prjxray-db.git
14. git checkout k325
15. popd
16. python3 xilinx/python/bbaexport.py --device xc7k325tffg676-1 --bba xilinx/xc7k325tffg676-1.bba
17. build/bbasm --l xilinx/xc7k325tffg676-1.bba xilinx/xc7k325tffg676-1.bin
18. sudo mkdir -p /usr/local/share/nextpnr/xilinx-chipdb
19. sudo ln -s $PWD/xilinx/external/prjxray-db /usr/local/share/nextpnr/
20. sudo cp xilinx/xc7k325tffg676-1.bin /usr/local/share/nextpnr/xilinx-chipdb/
21. Change directory to this project
22. ./makeit.sh

Note: Everytime you change the installation of nextpnr-xilinx you will have to regenerate the chipdb,
because the chipdb does not seem to be compatible between different binaries of nextpnr-xilinx
