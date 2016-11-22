here are a few pre-rolled community versions of vagrant boxes. I found this one [1] and the only thing I needed to do to run a mysql vagrant box with host accessibility was expose the forwarded guest ports.

For Allstate if you're looking to use vagrant for the larger enterprise you'll probably want to roll your own boxes, the path that Luke posited, so that you can certify what is going into a vagrant box for security purposes.

Creating a base box is fairly straight forward [2]. I've used Docker for container creation [3] and found it quite easy and enjoyable.

Have a safe, uneventful flight, filled with a lot of fun hacking and learning!

[1] Full vagrant file
Vagrant.configure("2") do |config|
  config.vm.box = "fnando/hellobits-trusty64"
  config.vm.network "forwarded_port", guest: 3306, host: 13306
end

[2] https://www.vagrantup.com/docs/boxes/base.html

[3] https://github.com/gfoster-pivotal/talks/blob/master/core-practices/how-to-pair/pairing-demo/tools/docker/Dockerfile
