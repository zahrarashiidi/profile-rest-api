Vagrant.configure("2") do |config|
  # استفاده از Ubuntu Jammy 64
  config.vm.box = "ubuntu/jammy64"

  # Synced folder بین ویندوز و ماشین مجازی
  config.vm.synced_folder ".", "/vagrant"

  # Port forwarding برای Django
  config.vm.network "forwarded_port", guest:8080, host: 8080, host_ip: "127.0.0.1"

  # Provisioning با Shell
  config.vm.provision "shell", inline: <<-SHELL
    # به‌روزرسانی پکیج‌ها
    sudo apt-get update
    sudo apt-get -y upgrade

    # نصب Python و ابزارهای ضروری
    sudo apt-get install -y python3 python3-dev python3-pip sqlite3 build-essential libssl-dev libffi-dev

    # ارتقا pip
    sudo pip3 install --upgrade pip

    # نصب virtualenv و virtualenvwrapper
    sudo pip3 install virtualenv virtualenvwrapper

    # تنظیم virtualenvwrapper در bashrc
    if ! grep -q VIRTUALENV_ALREADY_ADDED /home/vagrant/.bashrc; then
        echo "# VIRTUALENV_ALREADY_ADDED" >> /home/vagrant/.bashrc
        echo "WORKON_HOME=~/.virtualenvs" >> /home/vagrant/.bashrc
        echo "PROJECT_HOME=/vagrant" >> /home/vagrant/.bashrc
        echo "source /usr/local/bin/virtualenvwrapper.sh" >> /home/vagrant/.bashrc
    fi
  SHELL
end
