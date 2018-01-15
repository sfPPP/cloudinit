# cloudinit
cloudinit相关
cloudinit是干什么的：
  cloudinit用于在linux镜像创建实例时对实例进行初始化(windows系统中是cloudbase-init)
cloudinit的数据源： 
  metadata （元数据）：是键值对形式
      获取方法：   
              1. 利用metadata restful 服务
                    利用openstack提供的restful借口，虚拟机通过rest api 来获取metadata，该服务是由nova-api-metadata组件提供的。
                    虚拟机会像169.254.169.254:80发送请求。
                    例：http://169.254.169.254/openstack/2015-10-15/meta_data.json[root@test-init ~]# curl http://169.254.169.254/openstack/2015-10-15/meta_data.json
                    命令行执行 curl http://169.254.169.254/openstack/2015-10-15/meta_data.json
                    返回：
                      {"random_seed": "blabla(很长一段）=",
                          uuid": "75b60f20-47e1-42e5-8cfe-0d7e0d0d2fe1", 
                          "availability_zone": "nova", 
                          "hostname": "test-init.testdomain", 
                          "launch_index": 0, 
                          "project_id": "3f1a8be048ab4cc4b37de96125e17e6a",
                          "name": "test_init"}
                   
                2.利用config drive
                     config drive机制是指 OpenStack 将 metadata 信息写入虚拟机的一个特殊的配置设备中，然后在虚拟机启动时，
                          自动挂载并读取 metadata 信息，从而达到获取 metadata 的目的
                          例如, 初始化定制 Openstack 默认支持的 Libvirt 虚拟机配置时, OpenStack 就会将 metadata 写入虚拟机的 vdisk 文件中, 
                              并将 vdisk 指定为 cdrom 设备.
                     以 libvirt 为例：OpenStack 会将 metadata 写入 libvirt 的虚拟磁盘文件中，并指示 libvirt 将其虚拟为 cdrom 设备。
                     另一方面，虚拟机在启动时，客户端户操作系统中的 cloud-init 会去挂载并读取该设备，然后根据所读取出的内容对虚拟机进行配置
                     
               
                     
                     
  userdata(用户自定义数据)：
            userdata是用户在创建虚拟机时在openstackdashboard上传入的数据
            
  

