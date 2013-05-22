Vagrant.configure('2') do |config|
  config.vm.box = ENV.fetch('BOX', 'debian-6.0')
  config.vm.hostname = 'ruby-pkg'

  config.vm.provider :virtualbox do |v|
    v.customize ['modifyvm', :id, '--memory', 2048]
  end

  config.vm.provider :vmware_fusion do |v|
    v.vmx['memsize'] = 2048
  end

  # Configure Vagrant plugins.
  # See the README.md for installation instructions.
  config.berkshelf.enabled = true
  config.omnibus.chef_version = :latest

  # Install Ruby and other fpm dependencies in a separate run
  # to ensure that Ohai data is accurate
  config.vm.provision :chef_solo do |chef|
    chef.log_level = :debug if ENV['DEBUG']

    chef.add_recipe 'ruby_pkg::fpm_dependencies'
  end

  # Build and package the specified Ruby package
  config.vm.provision :chef_solo do |chef|
    chef.log_level = :debug if ENV['DEBUG']

    chef.add_recipe 'ruby_pkg'
    chef.json = {
      :ruby_pkg => {
        :pkg_dir      => '/vagrant/pkg',
        :ruby_version => ENV['VERSION'],
        :interation   => ENV['ITERATION'],
        :maintainer   => ENV['MAINTAINER']
      }
    }
  end
end