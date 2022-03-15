# change-docker-drive-location-wsl2

Steps for the process

1. Quit Docker Desktop
2. Open Command Prompt (or PowerShell) run with administrator
3. List existing WSL storages
  ```
  wsl --list -v
  ```
4. Turn off WSL
  ```
  wsl  --shutdown
  ```
5. Create following path (with all subfolders):
  ```
  mkdir D:\Docker\wsl\data\
  ```
6. Export containers and their data. This step can actually take some time depending on the size of the original ext4.vhdx file.
  ```
  wsl --export docker-desktop-data "D:\Docker\wsl\data\docker-desktop-data.tar"
  ```
 
7. Unregister the container data from WSL. It will also automatically delete the ext4.vhdx from original location.
  ```
  wsl --unregister docker-desktop-data
  ```
  
8. Import the container data, but keep it into another location (i.e. on drive D: as defined above). This will automatically create ext4.vhdx file from the backup.
  ```
  wsl --import docker-desktop-data "D:\Docker\wsl\data" "D:\Docker\wsl\data\docker-desktop-data.tar" --version 2
  ```

9. Delete the exported .tar file: D:\Docker\wsl\data\docker-desktop-data.tar
10. Start Docker Desktop and run your containers.
