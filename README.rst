*****
devip
*****

If you rely on IP-based authentication for accessing external services and work from remote locations often, you can use the *devip cli* to add your public IP address to the allowed origins with a simple command:

.. code-block:: bash

    $ devip move

When you move to a new location, by running the same command your previous temporary IP will be removed from the exceptions and the current one will be added. To make it permanent run the same command with the `-p` option:

.. code-block:: bash

    $ devip move -p

Permanent IP addresses are not removed when you switch locations. Also the cli will not remove IPs it doesn't have locally saved so your previous rules will not be modified. To see the list of saved IPs, run the following command:

.. code-block:: bash

    $ devip show

Sample output:

.. code-block:: bash

    Show all IP addresses...
    Temporary IPs:
        * 1.2.3.4/32
    Permanent IPs:
        No records

To clear temporary IPs:

.. code-block:: bash

    $ devip clear -t

To start managing an existing temporary IP:

.. code-block:: bash

    $ devip add -t -a 1.2.3.4

To stop managing an existing temporary IP:

.. code-block:: bash

    $ devip remove -t -a 1.2.3.4

By running the *move* subcommand again, all existing IPs added to the temporary list except your current one will be removed from the remote service exceptions, but remain saved locally for your reference.

----

Currently there is only support for AWS EC2 Security Groups, but plug-ins for other services can be easily added by adding a new module under the **/services** package directory and implementing the following 3 abstract methods: *get_service_ips*, *allow_ip* and *revoke_ip* similar to the provided *AmazonWebService* class.

To setup the *aws* service run the following command:

.. code-block:: bash

    $ devip setup -s aws

Sample output:

.. code-block:: bash

    Set up aws...
    Enter aws profile (default): [enter]
    Enter aws security_group: sg-1234abcd

Installation
************

.. code-block:: bash

    $ pip install devip
