Redis on Windows
================
let's start ...
This project contains the binary releases of MS Open Tech redis port of windows as well as a vagrant configuration for redis letting you run the native version of Redis in a Virtual Box VM.

Whilst it's recommended to use [Redis](http://redis.io) on Linux in production, it is often useful for developers on Windows platforms to have their own local version of redis running to develop with. 

The 2 most popular ways of running redis on windows is to use the binary releases of [Microsoft's native port of redis](https://github.com/msopentech/redis), but as this is an unofficial port it always lags behind the latest official development of redis on linux/OSX. 

Thanks to [Vagrant](http://www.vagrantup.com/) you can also run the latest linux version inside a Virutal Box Linux VM, which as it lets you run the official native version of redis, is our preferred approach:

## Running the latest version of Redis with Vagrant

#### 1. [Install Vagrant on Windows](http://docs.vagrantup.com/v2/getting-started/)

#### 2. Download the [vagrant-redis.zip](https://raw.github.com/ServiceStack/redis-windows/master/downloads/vagrant-redis.zip) vagrant configuration

    wget https://raw.github.com/ServiceStack/redis-windows/master/downloads/vagrant-redis.zip

#### 3. Extract `vagrant-redis.zip` in any folder, e.g. in `c:\vagrant-redis`

#### 4. Launch the Virtual Box VM with `vagrant up`

    cd c:\vagrant-redis
    vagrant up

This will launch a new Ubuntu VM instance inside Virtual Box that will automatically install and start the latest stable version of redis.

_The vagrant configuration was originally from [JasonPunyon/redishobo](https://github.com/JasonPunyon/redishobo) and has been modified to use the latest stable release of Redis._

## Running Microsoft's native port of Redis

These 64-bit binary releases are created by building the [Microsoft's native port of redis](https://github.com/msopentech/redis) which have also been published on [NuGet](http://www.nuget.org/packages/redis-64), but as it's more convenient we provide a zip of the 64-bit binaries here.

#### MS Open Announcements

  - [Redis on Windows release notes](https://raw.githubusercontent.com/MSOpenTech/redis/2.8/Redis%20on%20Windows%20Release%20Notes.md)
  - [MSOpenTech's Redis on Windows](https://github.com/ServiceStack/redis-windows/blob/master/docs/msopentech-redis-on-windows.md)
  - [Updates Released for Redis on Windows (2.8.4)](http://msopentech.com/blog/2014/03/24/updates-released-redis-windows/)

### Current Version: 2.8.21 r01 (July 29, 2015)

#### 1. Download the [redis64-latest.zip](https://github.com/ServiceStack/redis-windows/raw/master/downloads/redis-latest.zip) native 64bit Windows port of redis

    wget https://raw.github.com/ServiceStack/redis-windows/master/downloads/redis64-latest.zip

#### 2. Extract `redis64-latest.zip` in any folder, e.g. in `c:\redis`

#### 3. Run the `redis-server.exe` using the local configuration

    cd c:\redis
    redis-server.exe redis.conf

#### 4. Run `redis-cli.exe` to connect to your redis instance

    cd c:\redis
    redis-cli.exe

#### 5. Start playing with redis :)

    redis 127.0.0.1:6379> SET foo bar
    OK
    redis 127.0.0.1:6379> KEYS *
    1) "foo"
    redis 127.0.0.1:6379> GET foo
    "bar"
    redis 127.0.0.1:6379>

------

The MSOpenTech of Redis adds some useful extensions for better integration with Windows:

#### Running Redis as a Service

In order to better integrate with the Windows Services model, new command line arguments have been introduced to Redis. These service arguments require an elevated user context in order to connect to the service control manager. If these commands are invoked from a non-elevated context, Redis will attempt to create an elevated context in which to execute these commands. This will cause a User Account Control dialog to be displayed by Windows and may require Administrative user credentials in order to proceed.

#### Installing the Service

    --service-install

This must be the first argument on the redis-server command line. Arguments after this are passed in the order they occur to Redis when the service is launched. The service will be configured as Autostart and will be launched as "NT AUTHORITY\NetworkService". Upon successful installation a success message will be displayed and Redis will exit.
This command does not start the service.

For instance:

    redis-server --service-install redis.windows.conf --loglevel verbose

#### Uninstalling the Service

    --service-uninstall

This will remove the Redis service configuration information from the registry. Upon successful uninstallation a success message will be displayed and Redis will exit.
This does command not stop the service.  

For instance:

    redis-server --service-uninstall

#### Starting the Service

    --service-start

This will remove the Redis service configuration information from the registry. Upon successful uninstallation a success message will be displayed and Redis will exit.

For instance:  

    redis-server --service-start

#### Stopping the Service

    --service-stop

This will stop the Redis service. Upon successful termination a success message will be displayed and Redis will exit.

For instance:

    redis-server --service-stop

#### Naming the Service

    --service-name name

This optional argument may be used with any of the preceding commands to set the name of the installed service. This argument should follow the service-install, service-start, service-stop or service-uninstall commands, and precede any arguments to be passed to Redis via the service-install command. 
The following would install and start three separate instances of Redis as a service:

    redis-server --service-install –service-name redisService1 –port 10001
    redis-server --service-start –service-name redisService1
    redis-server --service-install –service-name redisService2 –port 10002
    redis-server --service-start –service-name redisService2
    redis-server --service-install –service-name redisService3 –port 10003
    redis-server --service-start –service-name redisService3

## [Configure Redis Sentinel Servers](https://github.com/ServiceStack/redis-config)

[![Instant Redis Setup](https://raw.githubusercontent.com/ServiceStack/Assets/master/img/redis/instant-sentinel-setup.png)](https://github.com/ServiceStack/redis-config)

See the
[redis config project](https://github.com/ServiceStack/redis-config) for a quick way to setup up 
the minimal 
[highly available Redis Sentinel configuration](https://github.com/ServiceStack/redis-config/blob/master/README.md#3x-sentinels-monitoring-1x-master-and-2x-slaves)
including start/stop scripts for instantly running multiple redis instances on a single (or multiple) 
Windows, OSX or Linux servers. 
26733
2661
21900
23565
31806
1816
27475
9446
2608
21891
12475
23193
31233
1283
6176
31198
25649
506
26080
5537
4403
24184
9003
761
20839
21441
17944
374
29611
32131
9337
14607
8151
29591
18868
29447
31870
21806
20655
5288
20375
32447
25425
29445
28130
19780
14244
716
17751
1810
24234
3664
20271
12990
32652
16522
15397
17775
6832
20998
4851
17076
28229
5816
8323
425
14369
11586
1978
18841
6536
17813
21808
849
23484
21353
18496
25040
8611
24915
13180
6920
19322
28350
11268
26809
30849
25902
15581
404
7516
12514
23480
15483
18918
9341
3146
21269
2072
8172
17515
20048
8455
21306
6719
9581
10511
10323
3167
18378
8411
12090
11102
14841
3865
20015
2350
16627
6848
14827
5613
10739
18539
30919
22049
12239
19830
13087
15480
6638
4798
32726
30107
12023
6307
31440
10120
4166
3416
17404
23887
30601
19187
11357
19762
5989
4973
24003
20853
2652
12633
450
6122
15318
1181
753
18215
27802
11751
22611
18231
9886
26131
31985
23897
2089
24208
22214
26034
12927
26113
24176
11151
24281
32610
14285
13118
16585
25406
4806
14211
14326
7696
15162
5568
29851
29485
12234
13940
4991
1839
8556
15705
19037
9421
11807
31260
31705
7463
28714
25916
22274
28235
15876
13593
9381
2995
26648
16706
372
10604
29963
1039
18851
6302
31760
15903
10491
17205
3541
24792
10878
23442
6050
20234
24639
27441
32616
20582
31260
28684
18153
6725
21815
12085
7022
59
25534
1663
17189
31439
1034
23469
4029
25854
185
3954
17849
7842
22507
18414
1756
1334
20402
26258
9821
30326
27868
12205
21330
32198
2210
28325
14066
5141
8058
18103
22905
27208
26979
