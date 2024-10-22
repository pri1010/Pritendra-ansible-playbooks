---
# File: install_service.yml
# Description: Playbook to install and start a service
# Usage: ansible-playbook install_service.yml

- name: Install and Start Service
  hosts: localhost
  become: true

  vars:
    # Define your service variables here
    service_name: httpd
    package_name: httpd

  tasks:
    - name: Install the service
      package:
        name: "{{ package_name }}"
        state: present
      register: install_status

    - name: Start the service
      service:
        name: "{{ service_name }}"
        state: started
        enabled: yes
      register: service_status

    - name: Display installation status
      debug:
        msg: "Service installation completed successfully"
      when: install_status is succeeded

    - name: Display service status
      debug:
        msg: "Service started successfully"
      when: service_status is succeeded


For Ubuntu/Debian version:


---
# File: install_service_ubuntu.yml
# Description: Playbook to install and start a service on Ubuntu
# Usage: ansible-playbook install_service_ubuntu.yml

- name: Install and Start Service
  hosts: localhost
  become: true

  vars:
    # Define your service variables here
    service_name: apache2
    package_name: apache2

  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes
        cache_valid_time: 3600

    - name: Install the service
      apt:
        name: "{{ package_name }}"
        state: present
      register: install_status

    - name: Start the service
      service:
        name: "{{ service_name }}"
        state: started
        enabled: yes
      register: service_status

    - name: Display installation status
      debug:
        msg: "Service installation completed successfully"
      when: install_status is succeeded

    - name: Display service status
      debug:
        msg: "Service started successfully"
      when: service_status is succeeded
