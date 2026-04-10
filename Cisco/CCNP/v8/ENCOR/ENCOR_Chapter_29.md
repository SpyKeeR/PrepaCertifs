![](media/image1.jpg)

> Chapter 29: Introduction to
>
> Automation Tools
>
> Instructor Materials
>
> CCNP Enterprise: Core Networking
>
> Chapter 29 Content
>
> **This chapter covers the following content:**
>
> • **Embedded Event Manager (EEM)** - This section illustrates common
> use cases and operations of the on-box EEM automation tool as well as
> the Tcl scripting engine.
>
> • **Agent-Based Automation Tools** - This section examines the
> benefits and operations of the various agent-based automation tools.
>
> • **Agentless Automation Tools** - This section examines the benefits
> and operations of the various agentless automation tools.
>
> This chapter is intended to provide a high-level overview of some of
> the most common configuration management and automation tools that are
> available.
>
> Embedded Event Manager
>
> • Embedded Event Manager (EEM) is a very flexible and powerful Cisco
> IOS tool. EEM
>
> allows engineers to build software applets that can automate many
> tasks.
>
> • EEM enables you to build custom scripts using Tcl. Scripts can
> automatically execute
>
> based on the output of an action or an event on a device.
>
> • EEM is all contained within the local device. There is no need to
> rely on an external scripting engine or monitoring device in most
> cases.
>
> • This section will cover EEM applets, EEM and Tcl scripts, and EEM
> summary.
>
> EEM Event Detectors
>
> ![](media/image2.jpg)Figure 29-1 illustrates some EEM event detectors
> and how they interact with the IOS subsystem.
>
> • EEM applets are composed of multiple building blocks. This chapter
> focuses on two of the primary building blocks that make up EEM
> applets: events and actions.
>
> • EEM applets use a similar logic to the if-then statements used in
> some of the common programming languages (for instance, if an event
> happens, then an action is taken).

**Figure 29-1**

*EEM Event Detectors*

© 2016 Cisco and/or its affiliates. All rights reserved. Cisco
Confidential 4

> EEM Applets
>
> Example 29-1 shows an applet that is looking for a specific syslog
> message, stating that the Loopback0 interface went down. If this
> specific syslog pattern is matched (an event) at least once, then the
> following actions will be taken:
>
> 1\. The Loopback0 interface will be shut down and brought back up.
>
> 2\. The router will generate a syslog message
>
> that says, "I've fallen, and I can't get up!"
>
> 3\. An email message that includes the output of the **show interface
> loopback0** command will be sent to the network administrator.

![](media/image3.jpg)

> Remember to include the **enable** and **configure terminal** commands
> at the beginning of actions within an applet.
>
> ![](media/image4.jpg)Debugging Output
>
> Based on the output from the **debug event manager action cli**
> command, you can see the actions taking place when the applet is
> running. Example 29-2 shows the applet being engaged when a user
> issues the **shutdown** command on the Loopback0 interface.
>
> (Entire output not shown.)
>
> ![](media/image6.png)CLI Patterns
>
> When certain commands are entered using the CLI, they trigger an EEM
> event within
>
> an applet. The configured actions then take place as a result of the
> CLI pattern being matched.
>
> Example 29-3 uses another common EEM applet to match the CLI pattern
> "write mem." When the applet is triggered, the following actions are
> invoked:
>
> 1\. The router generates a syslog message that says "Configuration
> File Changed! TFTP backup successful."
>
> 2\. The startup-config file is copied to a
>
> TFTP server.
>
> EEM Environment Values
>
> There are multiple ways to call out specific EEM environment values.
> Although it is possible to create custom names and values that are
> arbitrary and can be set to anything, it is good practice to use
> common and descriptive variables. Table 29-2 lists some of the email
> variables most commonly used in EEM.
>
> **Table 29-2** Common EEM Email Variables

> Tcl Scripts
>
> ![](media/image8.jpg)Example 29-4 shows how to manually execute an EEM
> applet that executes a Tcl script. It shows an EEM script configured
> with the **event none** command, which means there is no automatic
> event that the applet is monitoring, and
>
> this applet runs only when it is triggered manually. To manually run
> an EEM applet, the **event manager run** *applet-name* command must be
> used.

(Entire output not shown.)

> Script Contents
>
> ![](media/image10.jpg)Example 29-5 displays a snippet for the exact
> content of the ping.tcl script used in the manually triggered EEM
> applet in Example 29-4.
>
> To see the contents of a Tcl script that resides in flash memory,
> issue the **more** command followed by the file location and filename.
>
> The **more** command can be used to view all other text-based files
> stored in the local flash memory as well.
>
> EEM Summary
>
> The value in using automation and configuration management tools is
> the ability to move more quickly than is possible with manual
> configuration.
>
> Automation helps ensure that the level of risk due to human error is
> reduced by using proven automation methods.
>
> The following are some of the most common and repetitive
> configurations for which network
>
> operators leverage automation tools to increase speed and consistency:
>
> • Device name/IP address
>
> • Quality of service
>
> • Access list entries
>
> • Usernames/passwords
>
> • SNMP settings
>
> • Compliance
>
> Agent-Based Automation
>
> Tools
>
> • This section covers a number of agent-based tools as well as some of
> the key concepts to help network operators decide which tool best
> suits their environment and business use cases.
>
> Puppet
>
> • Puppet is a robust configuration management and automation tool.
> Puppet works with many different vendors and is a commonly used tools
> used for automation.
>
> • Puppet can be used during the entire lifecycle of a device,
> including initial deployment,
>
> configuration management, and repurposing and removing devices in a
> network.
>
> • Puppet uses a puppet master (server) to communicate with devices
> that have the puppet agent (client) installed locally on the device.
>
> • Changes and automation tasks are executed within the puppet console
> and then shared
>
> between the puppet master and puppet agents.
>
> • These changes or automation tasks are stored in the puppet database
> (PuppetDB) so that the tasks can be saved to be pushed out to the
> puppet agents at a later time.
>
> Figure 29-2 illustrates the communications path between the puppet
> master and the puppet agents, as well as the high-level architecture.
> The solid lines show the primary communications path, and the dotted
> lines indicate optional high availability.
>
> ![](media/image11.png)
>
> ![](media/image12.jpg)
>
> • Puppet agents communicate to the puppet master by using different
> TCP connections. TCP
>
> ports uniquely represent a communications path from an agent running
> on a device or node.
>
> • Puppet can periodically verify the configuration on devices. This
> can be set to any frequency that the network administrator deems
> necessary. If a configuration is changed, it can be alerted on, and
> automatically put back to the previous configuration.
>
> • There are three different installation types with Puppet. Table 29-3
> describes the scale
>
> differences between the different installation options.
>
> **Table 29-3 Puppet Installation Modes**

> • The recommended deployment is a monolithic installation, which
> supports up to 4000
>
> nodes. In a very large scale environment, best practices are high
> availability and centralized management. Administrators may need a
> master of masters (MoM) to manage the distributed puppet masters and
> their associated databases.
>
> • Large deployments also need compile masters, which are load-balanced
> Puppet servers.
>
> Figure 29-3 shows a typical large-scale enterprise deployment model of
> Puppet and its
>
> associated components.
>
> ![](media/image13.jpg)
>
> ![](media/image14.png)
>
> Puppet Modules
>
> Puppet modules contain these components:
>
> • Manifests
>
> • Templates
>
> • Files
>
> Manifests are the code that configures the clients or nodes running
> the puppet agent.
>
> Manifests are pushed to the devices using SSL and require certificates
> to ensure the security of communications between the puppet master and
> the puppet agents.
>
> Manifests can be saved as individual files and have a file extension
> .pp.
>
> One module called cisco_ios, contains many manifests and leverages SSH
> to connect to devices.
>
> Puppet Manifest
>
> • Example 29-6 shows an example of a manifest file, named
> NTP_Server.pp, that configures a Network Time Protocol (NTP) server on
> a Cisco Catalyst device.
>
> • This example shows that the NTP server IP address is configured as
> 1.2.3.4, and it uses VLAN 42 as the source interface. The line ensure
> =\> 'present' means that the NTP server configuration should be
> present in the running configuration of the Catalyst IOS device on
> which the manifest is running.
>
> ![](media/image15.jpg)
>
> • Puppet leverages a domain-specific language (DSL) as its
> "programming language." It is
>
> based on the Ruby language.
>
> • Example 29-7 shows a manifest file called MOTD.pp that is used to
> configure a message-of- the-day (MOTD) banner on Catalyst IOS devices.
>
> ![](media/image16.jpg)
>
> Chef
>
> • Chef is an open source configuration management tool. Chef is
> written in Ruby and Erlang,
>
> using Ruby for writing code within Chef.
>
> • Configuration management tools function in two different types of
> models: push and pull.
>
> • Chef is similar to Puppet in several ways:
>
> • Both have free open source versions available
>
> • Both have paid enterprise versions available
>
> • Both manage code that needs to be updated and stored
>
> • Both manage devices or nodes to be configured
>
> • Both leverage a pull model
>
> • Both function as a client/server model
>
> Chef's Structure
>
> • Chef's structure, terminology, and core components are different
> from those of Puppet.
>
> • Figure 29-4 illustrates the high-level architecture of Chef and the
> communications path
>
> between the various areas within the Chef environment.
>
> ![](media/image17.jpg)**Figure 29-4**
>
> *High-Level Chef Architecture*
>
> Chef Components
>
> Although the core concepts of Puppet and Chef are similar, the
> terminology differs. Whereas Puppet has modules and manifests, Chef
> has cookbooks and recipes. Table 29-4 compares the components of Chef
> and Puppet and provides a brief description of each component.
>
> **Table 29-4 Puppet and Chef Comparison**

> Chef Components (Cont.)
>
> • Code is created on the Chef workstation. This code is stored in a
> file called a recipe
>
> • Once a recipe is created on the workstation, it must be uploaded to
> the Chef server in order to be used in the environment. **knife** is
> the name of the command-line tool used to upload cookbooks to the Chef
> server.
>
> • The command to execute an upload is **knife upload** *cookbookname*.
>
> • The Chef server can be hosted locally on the workstation, hosted
> remotely on a server, or
>
> hosted in the cloud.
>
> There are four types of Chef server deployments:
>
> • **Chef Solo -** The Chef server is hosted locally on the
> workstation.
>
> • **Chef Client and Server -**This is a typical Chef deployment with
> distributed components.
>
> • **Hosted Chef -** The Chef server is hosted in the cloud.
>
> • **Private Chef -** All Chef components are within the same
> enterprise network.
>
> Chef Server
>
> • The Chef server sits in between the workstation and the nodes. All
> cookbooks are stored on the Chef server which holds all the tools
> necessary to transfer the node configurations to the Chef clients.
>
> • OHAI collects the current state of a node to send the information
> back to the Chef server through the Chef client service. The Chef
> server then checks to see if there is any new configuration that needs
> to be on the node by comparing the information from the OHAI service
> to the cookbook or recipe.
>
> • When a node needs a recipe, the Chef client service handles the
> communication back to the Chef server to signify the node's need for
> the updated configuration or recipe.
>
> **Recipe File**
>
> Example 29-8 shows a recipe file constructed in Ruby.
>
> Example 29-8 *Chef demo_insrall.rb Recipe*
>
> Cookbook Name:: cisco-cookbook
>
> Recipe\'\' demo_install
>
> Copyright (c) 2014 -2017 Cisco and/or its affiliates.
>
> \# Licensed under the Apache License, Version 2.0 (the \"License\");
>
> y011 m.:IY not IIAP t.h i A fi 1fP PXPpt:. in nmpl i.::ln PW1 t.h thP
> f.1 C\":PnA,:).
>
> You may obtain a copy of the Licen5e at
>
> http,//[www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)
>
> un1eaa required by applicable law or agreed to in writing, software
>
> distributed under the License is distributed on an \"AS ts• BASIS.
>
> WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
> implied.
>
> .tl: soo tho Liconao f or tho SPQCit ic l;mgu.;a.go govorniniJ
> PQrmiaaione and.
>
> limitations under the Licenae.
>
> In our recipes. due to the numbe r or dirrerent parameters, we prerer
> to align
>
> thO ; .r9Uft\\Qnta in ;t ainl)l :t column r;a.thor than tollowing
> rubocop 1**a** atylG .
>
> ·•1•·11\"
>
> CISCO
>
> Chef::Log . into(\'Demc: cieco_cocm:an:1_con r:ig prov:.d.el.-\' )
>
> ciseo comrn.and. coni!g 1lOOp4 2 1 dO
>
> .:a.e:ion :upd.:a.to
>
> UIUIW.UIJ \'
>
> inter!ace loopback42
>
> description Peering tor AS 4 2
>
> :.p .:a.dd.rgae 192.169.1 4J:/24
>
> eno
>
> ciaco_corvnmd_contig • sy:;tom-switchport-dGfd·.llt\' do
>
> VIIIIUcUUJ \'UU ttyttl.l:!ll. \[cl u :.Hl Wl l.L:h,l)Ul l.\'
>
> enO

![](media/image18.jpg)

> comrr..:a.na \' ro c:uro DIJP \'
>
> ona
>
> cioco_comma.nd_contig \'router_Ogp_4 2 \' ào
>
> action :update
>
> l..\"UI.IUI\....J-.1 °
>
> rcuc:.or ogp 4:l
>
> router id :!\>2.160 .1.4 2 adc1reo3 !\'aoily ipv4: unica3t
>
> network 1.o. c.0/8
>
> f \... J I\"\' I - f lblll \... H I \.... I \_ ÎC: fi)IJI\....
> -III;.tp hyp-K .-..I.ÎCK
>
> no1gni\>Or 10.1.1.1
>
> SaltStack Overview
>
> • SaltStack is built on Python with a Python interface so a user can
> program directly to
>
> SaltStack by using Python code.
>
> • However, most of the instructions or states that get sent out to the
> nodes are written in
>
> YAML or a DSL. These are called Salt formulas.
>
> • Another key difference from Puppet and Chef is SaltStack's overall
> architecture. SaltStack uses systems, which are divided into various
> categories. SaltStack has masters and minions.
>
> • SaltStack uses a distributed messaging platform called 0MQ (ZeroMQ).
> SaltStack is an event-driven technology that has components called
> reactors and beacons. A reactor lives on the master and listens for
> any type of changes in the node or device that differ from the desired
> state or configuration.
>
> • Beacons live on minions. If a configuration changes on a node, a
> beacon notifies the reactor on the master. This is the remote
> execution system and it helps determine whether the configuration is
> in the appropriate state on the minions. These actions are called jobs
> which when executed can be stored in an external database.
>
> • SaltStack uses pillars and grains to control state and send
> configuration changes. SaltStack grains are run on the minions to
> gather system information to report back to the master. This
> information is typically gathered by the salt-minion daemon. Grains
> can provide specifics to the master about the host.
>
> • Pillars store data that a minion can retrieve from the master.
> Minions can be assigned to pillars.
>
> • Data can be stored for a specific node inside a pillar, keeping it
> separate from any other node that is not assigned to this particular
> pillar. Confidential data can be secured and only shared with assigned
> minions.
>
> ![](media/image19.jpg)SaltStack Architecture
>
> • SaltStack can scale to a very large number of devices. SaltStack
> also has an enterprise version and a GUI called SynDic.
>
> • Figure 29-5 shows the overall architecture of SaltStack and its
> associated components.
>
> ![](media/image20.jpg)SaltStack CLI
>
> • SaltStack has its own DSL. The SaltStack command structure contains
> *targets*, *commands*, and *arguments*.
>
> • The target is the desired system that the command should run.
>
> • The command structure uses the module.function syntax followed by
> the argument.
>
> • An argument provides detail to the module and function that is being
> called on in the command.
>
> • Figure 29-6 shows the correct SaltStack syntax as well as a command
> called cmd.run.
>
> Agentless Automation Tools
>
> • This section covers a variety of agentless tools as well as some of
> the key concepts to help network operators decide which tool best
> suits their environment and business use cases.
>
> Ansible Overview
>
> ![](media/image21.jpg)• Ansible is an automation tool that is capable
> of automating cloud provisioning, deployment of applications, and
> configuration management.
>
> • Ansible is agentless, so no software needs to be installed on the
> client machines. Ansible communicates using SSH. Ansible can use
> built-in authorization escalation when it needs to raise the level of
> administrative control.
>
> • Ansible sends all requests from a control station. Figure 29-8
> illustrates the Ansible workflow.
>
> Ansible Playbook Components
>
> • Ansible uses playbooks to deploy configuration changes or retrieve
> information from hosts within a network. An Ansible playbook is a
> structured sets of instructions. An Ansible playbook contains multiple
> plays, and each play contains the tasks that each player must
> accomplish in order for the particular play to be successful.
>
> • Table 29-5 describes the components used in Ansible and provides
> some commonly used examples of them.
>
> Ansible Playbooks in YAML
>
> ![](media/image22.png)![](media/image23.jpg)• Ansible playbooks are
> written using YAML (Yet Another Markup Language). Ansible YAML files
> usually begin with a series of three dashes (\-\--) and end with a
> series of three periods (...). Example 29-9 shows a YAML file that
> contains a list of musical genres.
>
> • YAML uses dictionaries that are similar to JSON dictionaries as they
> also use key/value pairs. Example
>
> 29-10 shows a YAML dictionary containing an employee record.
>
> Ansible has a CLI tool that can be used to run playbooks or ad hoc CLI
> commands on targeted hosts. This tool has very specific commands that
> you need to use to enable automation. The table below shows the most
> common Ansible CLI commands and associated use cases.

> ![](media/image24.png)Ansible Configuration Example
>
> • Example 29-14 shows an alternative version of the
> ConfigureInterface.yaml playbook named EIGRP_Configuration\_
> Example.yaml, with EIGRP added,
>
> along with the ability to save the configuration by issuing a "write
> memory."
>
> • These tasks are accomplished by leveraging the ios_command module in
> Ansible. This playbook adds the configuration shown here to the
> CSR1KV-1 router.
>
> Puppet Bolt
>
> • Puppet Bolt allows you to leverage the power of Puppet without
> having to install a puppet master or puppet agents on devices or
> nodes.
>
> • It connects to devices by using SSH or WinRM connections. Puppet
> Bolt is an open
>
> source tool that is based on the Ruby language and can be installed as
> a single package.
>
> • Puppet Bolt allows you to execute a change or configuration
> immediately and then validate it. There are two ways to use Puppet
> Bolt:
>
> • **Orchestrator-driven tasks** - Orchestrator-driven tasks can
> leverage the Puppet architecture to use services to connect to
> devices. This design is meant for large- scale environments.
>
> • **Standalone tasks** - Standalone tasks are for connecting directly
> to devices or nodes to execute tasks and do not require any Puppet
> environment or components to be
>
> set up in order to realize the benefits and value of Puppet Bolt.

![](media/image25.jpg)

> • Individual commands can be run from the command line by using the
> command **bolt command run**
>
> *command name* followed by the list of devices to run the command
> against.
>
> • After a script is built, execute it from the command line against
> the remote devices that need to be configured, using the command
> **bolt script run** *script name* followed by the list of devices to
>
> run the script against. Figure 29-14 shows a list of some of the
> available commands for Puppet Bolt.
>
> • Puppet Bolt tasks use an API to retrieve data between Puppet Bolt
> and the remote device.
>
> • Tasks are part of the Puppet modules and use the naming structure
>
> *modulename*::*taskfilename*.
>
> • Tasks can be called from the command line much like commands and
> scripts. You use the command bolt task run
> *modulename*::*taskfilename* to invoke these tasks from the command
> line.
>
> • The *modulename*::*taskfilename* naming structure allows the tasks
> to be shared with other users on Puppet Forge.
>
> • A task is commonly accompanied by a metadata file that is in JSON
> format. A JSON metadata file contains information about a task, how to
> run the task, and any comments about how the file is written.
>
> SaltStack Salt SSH (Server-Only Mode)
>
> • SaltStack offers an agentless option called Salt SSH that allows
> users to run Salt commands without having to install a minion on the
> remote device or node. The main requirements to use Salt SSH are that
> the remote system must have SSH enabled and Python installed.
>
> • Salt SSH can work in conjunction with the master/minion environment,
> or it can be used completely agentless across the environment. By
> default, Salt SSH uses roster files to store connection information
> for any host that doesn't have a minion installed. Example
>
> 29-16 shows the content structure of this file.
>
> ![](media/image26.png)
>
> Comparing Tools
>
> Table 29-7 provides a high-level comparison of the tools covered in
> this chapter.

> Prepare for the Exam

![](media/image27.jpg)
