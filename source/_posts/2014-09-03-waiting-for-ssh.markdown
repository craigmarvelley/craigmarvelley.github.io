---
layout: post
title: "Waiting for SSH"
date: 2014-09-03 19:17:18 +0000
comments: false
categories: ansible
---

**Update 2014/09/06** - Michael DeHaan [mentions on Twitter](https://twitter.com/laserllama/status/507325690610728962) that he adds in a few seconds of sleep with the pause module to ensure the SSH port is open.

I've spent the day provisioning a whole lot of EC2 instances with Ansible from a control machine in the cloud. This involves two stages: firstly an instance is launched, and then once SSH is available (using Ansible's `wait_for` module), the second stage of more detailed provisioning begins.

An issue I'd experienced a few times previously but had not been able to pinpoint, was that often the `wait_for` module failed to identify that SSH is ready. My Ansible task looked like this:

{% codeblock %}
{% raw %}
- name: Wait until SSH is available
  local_action: 
    module: wait_for 
    host: "{{ item.public_dns_name }}"
    port: 22 
    delay: 60 
    timeout: 320 
    state: started
  with_items: launched_instances.instances
{% endraw %}
{% endcodeblock %}

That task would often time out, but in such cases if I were to immediately try to SSH from the terminal it would succeed, which was odd indeed.

Today this behaviour was consistent, and I eventually realised that in the task I was using the instance's public DNS name, whereas when I was connecting via the terminal I used the public IP address. Indeed, changing the task to use the IP address seems to have made the whole thing a lot more reliable:

{% codeblock %}
{% raw %}
- name: Wait until SSH is available
  local_action: 
    module: wait_for 
    host: "{{ item.public_ip }}"
    port: 22 
    delay: 60 
    timeout: 320 
    state: started
  with_items: launched_instances.instances
{% endraw %}
{% endcodeblock %}

I'm guessing that on my Mac (where this was rarely an issue) the DNS cache updates quicker than it does on the control machine in EC2, where this problem was more frequent - using the explicit IP address renders the issue moot.
