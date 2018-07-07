## Configuration Management Database

Keeping configuration in a centralized [Configuration Management Database](https://en.wikipedia.org/wiki/Configuration_management_database) is a fundamental need within an organization to create automation.

A configuration management database should be the definitive reference for hosts/virtual machines/containers/users/groups/production configuration along with all related attributes and relations. This system should be flexible enough for other types of relational objects to be created for future use. Data should be in revision controlled files or a versioned database backend. The system will have apis which allow other applications and scripts to fetch and update data. Also including other relational data and attributes like configuration management roles, datacenters, ethernet addresses, ownership, machine physical locations in the system allows for DNS, DHCP, monitoring, inventory, automation, deployment, and other tools to automatically pull relevant information and auto generate their configs.

Once you have this system, the amount of data you can store in it is endless, everything from doing users and group management in a centralized place, to a repository of ssh keys, anything you’d need a centralized definitive reference for.

