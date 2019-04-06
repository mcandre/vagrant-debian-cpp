VERSION = '0.0.1'
PROVIDER = 'virtualbox'
ARCHITECTURES = ['amd64', 'i386', 'ppc64el']
BOX_NAMESPACE = 'mcandre'
BOX_BASENAME_AMD64 = 'vagrant-debian-cpp-amd64'
BOX_AMD64 = "#{BOX_BASENAME_AMD64}.box"
BOX_BASENAME_I386 = 'vagrant-debian-cpp-i386'
BOX_I386 = "#{BOX_BASENAME_I386}.box"
BOX_BASENAME_PPC64EL = 'vagrant-debian-cpp-ppc64el'
BOX_PPC64EL = "#{BOX_BASENAME_PPC64EL}.box"
SHORT_DESCRIPTION_AMD64 = 'a Vagrant box for building C/C++ binaries for GNU/Linux (Debian) x86_64'
SHORT_DESCRIPTION_I386 = 'a Vagrant box for building C/C++ binaries for GNU/Linux (Debian) x86'
SHORT_DESCRIPTION_PPC64EL = 'a Vagrant box for building C/C++ binaries for GNU/Linux (Debian) ppc64el'
VERSION_DESCRIPTION = 'Source: https://github.com/mcandre/vagrant-debian-cpp'

task :default => 'test'

task :box_amd64 => [
    "amd64#{File::SEPARATOR}Vagrantfile",
    "amd64#{File::SEPARATOR}bootstrap.sh",
    "amd64#{File::SEPARATOR}export.Vagrantfile",
    :clean_box_amd64
] do
    sh 'vagrant up',
        :chdir => 'amd64'
    sh "vagrant package --output #{BOX_AMD64} --vagrantfile export.Vagrantfile",
        :chdir => 'amd64'
    sh "chown $SUDO_USER: #{BOX_AMD64}",
        :chdir => 'amd64'
end

task :box_i386 => [
    "i386#{File::SEPARATOR}Vagrantfile",
    "i386#{File::SEPARATOR}bootstrap.sh",
    "i386#{File::SEPARATOR}export.Vagrantfile",
    :clean_box_i386
] do
    sh 'vagrant up',
        :chdir => 'i386'
    sh "vagrant package --output #{BOX_I386} --vagrantfile export.Vagrantfile",
        :chdir => 'i386'
    sh "chown $SUDO_USER: #{BOX_I386}",
        :chdir => 'i386'
end

task :box_ppc64el => [
    "ppc64el#{File::SEPARATOR}Vagrantfile",
    "ppc64el#{File::SEPARATOR}bootstrap.sh",
    "ppc64el#{File::SEPARATOR}export.Vagrantfile",
    :clean_box_ppc64el
] do
    sh 'vagrant up --provider libvirt',
        :chdir => 'ppc64el'
    sh 'chmod -R a+r /var/lib/libvirt/images'
    ENV['VAGRANT_LIBVIRT_VIRT_SYSPREP_OPERATIONS'] = 'defaults,-ssh-userdir,-ssh-hostkeys,-lvm-uuids'
    sh "vagrant package --output #{BOX_PPC64EL} --vagrantfile export.Vagrantfile",
        :chdir => 'ppc64el'
    sh "chown $SUDO_USER: #{BOX_PPC64EL}",
        :chdir => 'ppc64el'
end

task :boxes => [:box_amd64, :box_i386, :box_ppc64el] do
end

task :import_amd64 => [] do
    sh "vagrant box add --force --name #{BOX_NAMESPACE}/#{BOX_BASENAME_AMD64} #{BOX_AMD64}",
        :chdir => 'amd64'
end

task :import_i386 => [] do
    sh "vagrant box add --force --name #{BOX_NAMESPACE}/#{BOX_BASENAME_I386} #{BOX_I386}",
        :chdir => 'i386'
end

task :import_ppc64el => [] do
    sh "vagrant box add --force --name #{BOX_NAMESPACE}/#{BOX_BASENAME_PPC64EL} #{BOX_PPC64EL}",
        :chdir => 'ppc64el'
end

task :import => [:import_amd64, :import_i386, :import_ppc64el] do
end

task :test_amd64 => [
    "amd64#{File::SEPARATOR}test#{File::SEPARATOR}Vagrantfile",
    "amd64#{File::SEPARATOR}test#{File::SEPARATOR}hello.cpp"
] do
    sh 'vagrant up',
        :chdir => "amd64#{File::SEPARATOR}test"
    sh 'vagrant ssh -c "cd /vagrant && clang++ -o hello hello.cpp && ./hello"',
        :chdir => "amd64#{File::SEPARATOR}test"
end

task :test_i386 => [
    "i386#{File::SEPARATOR}test#{File::SEPARATOR}Vagrantfile",
    "i386#{File::SEPARATOR}test#{File::SEPARATOR}hello.cpp"
] do
    sh 'vagrant up',
        :chdir => "i386#{File::SEPARATOR}test"
    sh 'vagrant ssh -c "cd /vagrant && clang++ -o hello hello.cpp && ./hello"',
        :chdir => "i386#{File::SEPARATOR}test"
end

task :test_ppc64el => [
    "ppc64el#{File::SEPARATOR}test#{File::SEPARATOR}Vagrantfile",
    "ppc64el#{File::SEPARATOR}test#{File::SEPARATOR}hello.cpp"
] do
    sh 'vagrant up --provider libvirt',
        :chdir => "ppc64el#{File::SEPARATOR}test"
    sh 'vagrant ssh -c "cd /vagrant && clang++ -o hello hello.cpp && ./hello"',
        :chdir => "ppc64el#{File::SEPARATOR}test"
end

task :test => [:test_amd64, :test_i386, :test_ppc64el] do
end

task :publish_amd64 => [] do
    sh "vagrant cloud publish #{BOX_NAMESPACE}/#{BOX_BASENAME_AMD64} --force --release --short-description \"#{SHORT_DESCRIPTION_AMD64}\" --version-description \"#{VERSION_DESCRIPTION}\" #{VERSION} #{PROVIDER} #{BOX_AMD64}",
        :chdir => 'amd64'
end

task :publish_i386 => [] do
    sh "vagrant cloud publish #{BOX_NAMESPACE}/#{BOX_BASENAME_I386} --force --release --short-description \"#{SHORT_DESCRIPTION_I386}\" --version-description \"#{VERSION_DESCRIPTION}\" #{VERSION} #{PROVIDER} #{BOX_I386}",
        :chdir => 'i386'
end

task :publish_ppc64el => [] do
    sh "vagrant cloud publish #{BOX_NAMESPACE}/#{BOX_BASENAME_PPC64EL} --force --release --short-description \"#{SHORT_DESCRIPTION_PPC64EL}\" --version-description \"#{VERSION_DESCRIPTION}\" #{VERSION} #{PROVIDER} #{BOX_PPC64EL}",
        :chdir => 'ppc64el'
end

task :publish => [:publish_amd64, :publish_i386, :publish_ppc64el] do
end

task :clean_box_amd64 => [] do
    Dir.glob("amd64#{File::SEPARATOR}*.box").each { |path| File.delete path }
end

task :clean_amd64 => [:clean_box_amd64] do
    begin
        sh 'vagrant destroy -f', :chdir => 'amd64'
    rescue
    end

    begin
        sh 'vagrant destroy -f',
            :chdir => "amd64#{File::SEPARATOR}test"
    rescue
    end

    begin
        Dir.glob("amd64#{File::SEPARATOR}**#{File::SEPARATOR}.vagrant").each { |path| FileUtils.rm_r path }
    rescue
    end

    begin
        FileUtils.rm_r "amd64#{File::SEPARATOR}_tmp_package"
    rescue
    end
end

task :clean_box_i386 => [] do
    Dir.glob("i386#{File::SEPARATOR}*.box").each { |path| File.delete path }
end

task :clean_i386 => [:clean_box_i386] do
    begin
        sh 'vagrant destroy -f', :chdir => 'i386'
    rescue
    end

    begin
        sh 'vagrant destroy -f',
            :chdir => "i386#{File::SEPARATOR}test"
    rescue
    end

    begin
        Dir.glob("i386#{File::SEPARATOR}**#{File::SEPARATOR}.vagrant").each { |path| FileUtils.rm_r path }
    rescue
    end

    begin
        FileUtils.rm_r "i386#{File::SEPARATOR}_tmp_package"
    rescue
    end
end

task :clean_box_ppc64el => [] do
    Dir.glob("ppc64el#{File::SEPARATOR}*.box").each { |path| File.delete path }
end

task :clean_ppc64el => [:clean_box_ppc64el] do
    begin
        sh 'vagrant destroy -f', :chdir => 'ppc64el'
    rescue
    end

    begin
        sh 'vagrant destroy -f',
            :chdir => "ppc64el#{File::SEPARATOR}test"
    rescue
    end

    begin
        Dir.glob("ppc64el#{File::SEPARATOR}**#{File::SEPARATOR}.vagrant").each { |path| FileUtils.rm_r path }
    rescue
    end

    begin
        FileUtils.rm_r "ppc64el#{File::SEPARATOR}_tmp_package"
    rescue
    end
end

task :clean => [:clean_amd64, :clean_i386, :clean_ppc64el] do
end
