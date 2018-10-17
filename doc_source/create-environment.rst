.. Copyright 2010-2018 Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _create-environment:

####################################
Creating an Environment in |AC9long|
####################################

.. meta::
    :description:
        Describes how to create an environment in AWS Cloud9.

To create an |envfirstlong|, follow one of these sets of procedures, depending on how you plan to use |AC9|.

.. list-table::
   :widths: 1
   :header-rows: 0

   * - If you're not sure what to choose, we recommend :ref:`creating an EC2 environment <create-environment-main>`.

       Creating an |envec2| is the easiest option. |AC9| automatically creates and sets up a new |EC2| instance in your AWS account. 
       |AC9| then automatically connects that new instance to the |env| for you.

.. list-table::
   :widths: 1 2 1
   :header-rows: 1

   * - **Source code provided by**
     - **Development environment host provided by**
     - **Follow these procedures**
   * - You
     - |AC9|
     - This topic (:ref:`create an EC2 environment <create-environment-main>`)
   * - You
     - You
     - This topic (:ref:`create an SSH environment <create-environment-ssh>`)
   * - `Amazon Lightsail <https://aws.amazon.com/lightsail>`_ or you
     - You, by using |lightsail|
     - :ref:`Working with Amazon Lightsail Instances <lightsail-instances>`
   * - `AWS CodeStar <https://aws.amazon.com/codestar>`_ or you
     - |AC9|, by using |ACSlong|
     - :ref:`Working with AWS CodeStar Projects <codestar-projects>`
   * - You, by using `AWS CodePipeline <https://aws.amazon.com/codepipeline>`_
     - |AC9| or you
     - This topic (create an :ref:`EC2 <create-environment-main>` or :ref:`SSH <create-environment-ssh>` environment), and then see :ref:`Working with AWS CodePipeline <codepipeline-repos>`
   * - You, by using `AWS CodeCommit <https://aws.amazon.com/codecommit>`_
     - |AC9| or you
     - :ref:`AWS CodeCommit Sample <sample-codecommit>`
   * - You, by using `GitHub <https://github.com/>`_
     - |AC9| or you
     - This topic (create an :ref:`EC2 <create-environment-main>` or :ref:`SSH <create-environment-ssh>` environment), and then see the :ref:`GitHub Sample <sample-github>`
 
.. _create-environment-main:

Creating an |envec2title|
=========================

.. note:: Completing this procedure might result in charges to your AWS account. These include possible charges for |EC2|. For more information, see
   `Amazon EC2 Pricing <https://aws.amazon.com/ec2/pricing/>`_.

In this procedure, |AC9| creates an |envec2|, creates a new |EC2| instance, and then connects the |env| to this newly-created instance. 
|AC9| manages this instance's lifecycle, including starting, stopping, and restarting the instance as needed. If you ever delete this |env|, |AC9| automatically terminates this instance.

You can create an |envfirstec2| with the :ref:`AWS Cloud9 console <create-environment-console>` or with :ref:`code <create-environment-code>`.

.. _create-environment-console:

Creating an |envec2title| with the Console
-------------------------------------------

#. Make sure you completed the steps in :ref:`Express Setup <setup-express>` or :ref:`Team Setup <setup>` first, so that you can sign in to the |AC9| console and create |envplural|.
#. Sign in to the |AC9| console, at |AC9Console_link|.
#. After you sign in to the |AC9| console, in the top navigation bar, choose an AWS Region to create the |env| in. For a list of available AWS Regions, see 
   :aws-gen-ref:`AWS Cloud9 <rande.html#cloud9_region>` in the |AWS-gr|.

   .. image:: images/console-region.png
      :alt: AWS Region selector in the AWS Cloud9 console

#. If a welcome page is displayed, for :guilabel:`New AWS Cloud9 environment`, choose :guilabel:`Create environment`.
   Otherwise, choose :guilabel:`Create environment`.

   .. image:: images/console-welcome-new-env.png
      :alt: Choosing the Next step button if welcome page is displayed

   Or: 
   
   .. image:: images/console-new-env.png
      :alt: Choosing the Create environment button if welcome page is not displayed

#. On the :guilabel:`Name environment` page, for :guilabel:`Name`, type a name for your |env|.
#. To add a description to your |env|, type it in :guilabel:`Description`.
#. Choose :guilabel:`Next step`.
#. On the :guilabel:`Configure settings` page, for :guilabel:`Environment type`, choose :guilabel:`Create a new instance for environment (EC2)`.
#. For :guilabel:`Instance type`, choose an instance type with the amount of RAM and vCPUs you think you need for the kinds of tasks you want to do. Or leave the default choice.

   .. note:: Choosing instance types with more RAM and vCPUs might result in additional charges to your AWS account for |EC2|.

#. For :guilabel:`Cost-saving setting`, choose the amount of time until |AC9| shuts down the |EC2| instance for the 
   |env| after all web browser instances that are connect to the |IDE| for the |env| have been closed. Or leave the default choice.

   .. note:: Choosing a shorter time period might result in fewer charges to your AWS account. Likewise, choosing a longer time might result in more charges.

#. Expand :guilabel:`Network settings (advanced)`.
#. |AC9| uses |VPClong| (|VPC|) in your AWS account to communicate with the |EC2| instance that |AC9| creates for this |env|. Depending on how |VPC| is set up in your AWS account, do one of the following.

   .. list-table::
      :widths: 1
      :header-rows: 0

      * - If you're not sure what to choose, we recommend that you skip ahead to step 13 in this procedure.

          When you skip past :guilabel:`Network settings (advanced)` and leave the preselected default settings, 
          |AC9| attempts to automatically use the default VPC in your account with its single subnet.
    
   .. list-table::
      :widths: 2 3 1 3
      :header-rows: 1

      * - **Does your AWS account have a VPC with at least one subnet in that VPC?**
        - **Is the VPC you want AWS Cloud9 to use the default VPC in your account?**
        - **Does the VPC have a single subnet?**
        - **Do this**
      * - No
        - |mdash|
        - |mdash|
        - If no VPC exists, create one. To do this, choose :guilabel:`Create new VPC`, and then follow the 
          on-screen directions. For more information, see :ref:`vpc-settings-create-vpc`.
          
          If a VPC exists but has no subnet, create one. To do this, choose :guilabel:`Create new subnet`, 
          and then follow the on-screen directions. For more information, see :ref:`vpc-settings-create-subnet`.
      * - Yes
        - Yes
        - Yes
        - Skip ahead to the step 13 in this procedure. 
        
          When you skip past :guilabel:`Network settings (advanced)` and leave the preselected default settings, 
          |AC9| attempts to automatically use the default VPC in your account with its single subnet.
      * - Yes
        - Yes
        - No
        - For :guilabel:`Subnet`, choose the subnet you want |AC9| to use in the preselected default VPC. 
      * - Yes
        - No
        - |mdash|
        - For :guilabel:`Network (VPC)`, choose the VPC that you want |AC9| to use. 
          For :guilabel:`Subnet`, choose the subnet you want |AC9| to use in that VPC.

   For more information about these choices, see :doc:`Amazon VPC Settings <vpc-settings>`.

#. Choose :guilabel:`Next step`.
#. On the :guilabel:`Review` page, choose :guilabel:`Create environment`. Wait while |AC9| creates your |env|. 
   This can take several minutes.

After |AC9| creates your |env|, it displays the |AC9IDE| for the |env|.

If |AC9| doesn't display the |IDE| after at least five minutes, there might be a problem with your web browser, your AWS access permissions, the instance, or the associated
virtual private cloud (VPC). For possible fixes, see
:ref:`troubleshooting-env-loading` in *Troubleshooting*.

.. _create-environment-code:

Creating an |envec2title| with Code
-----------------------------------

To use code to create an |envec2| in |AC9|, call the |AC9| create |envec2| operation, as follows.

.. note:: Make sure you completed the steps in :ref:`Express Setup <setup-express>` or :ref:`Team Setup <setup>` first, so that you can create |envplural|.

.. list-table::
   :widths: 1 1
   :header-rows: 0

   * - |cli|
     - :AC9-cli:`create-environment-ec2 <create-environment-ec2>`
   * - |sdk-cpp|
     - :sdk-cpp-ref:`CreateEnvironmentEC2Request <LATEST/class_aws_1_1_cloud9_1_1_model_1_1_create_environment_e_c2_request>`, 
       :sdk-cpp-ref:`CreateEnvironmentEC2Result <LATEST/class_aws_1_1_cloud9_1_1_model_1_1_create_environment_e_c2_result>`
   * - |sdk-go|
     - :sdk-for-go-api-ref:`CreateEnvironmentEC2 <service/cloud9/#Cloud9.CreateEnvironmentEC2>`, 
       :sdk-for-go-api-ref:`CreateEnvironmentEC2Request <service/cloud9/#Cloud9.CreateEnvironmentEC2Request>`, 
       :sdk-for-go-api-ref:`CreateEnvironmentEC2WithContext <service/cloud9/#Cloud9.CreateEnvironmentEC2WithContext>`
   * - |sdk-java|
     - :sdk-java-api:`CreateEnvironmentEC2Request <com/amazonaws/services/cloud9/model/CreateEnvironmentEC2Request>`, 
       :sdk-java-api:`CreateEnvironmentEC2Result <com/amazonaws/services/cloud9/model/CreateEnvironmentEC2Result>`
   * - |sdk-js|
     - :sdk-for-javascript-api-ref:`createEnvironmentEC2 <AWS/Cloud9.html#createEnvironmentEC2-property>`
   * - |sdk-net|
     - :sdk-net-api-v3:`CreateEnvironmentEC2Request <items/Cloud9/TCreateEnvironmentEC2Request>`, 
       :sdk-net-api-v3:`CreateEnvironmentEC2Response <items/Cloud9/TCreateEnvironmentEC2Response>`
   * - |sdk-php|
     - :sdk-for-php-api-ref:`createEnvironmentEC2 <api-cloud9-2017-09-23.html#createenvironmentec2>`
   * - |sdk-python|
     - :sdk-for-python-api-ref:`create_environment_ec2 <services/cloud9.html#Cloud9.Client.create_environment_ec2>`
   * - |sdk-ruby|
     - :sdk-for-ruby-api-ref:`create_environment_ec2 <Aws/Cloud9/Client.html#create_environment_ec2-instance_method>`
   * - |TWPlong|
     - :TWP-ref:`New-C9EnvironmentEC2 <items/New-C9EnvironmentEC2>`
   * - |AC9| API
     - :AC9-api:`CreateEnvironmentEC2 <API_CreateEnvironmentEC2>`

.. _create-environment-ssh:

Creating an |envsshtitle|
=========================

You create an |envfirstssh| with the |AC9| console. (You cannot create an |envssh| with code.)

Prerequisites
-------------

* Make sure you completed the steps in :ref:`Express Setup <setup-express>` or :ref:`Team Setup <setup>`, so that you can sign in to the |AC9| console and create |envplural|.
* Identify an existing cloud compute instance (for example an |EC2| instance in your AWS account), or your own server, that you want |AC9| to connect to the |env|.
* The existing instance or your own server must be running Linux. |AC9| doesn't support Windows.
* You must be able to reach the existing instance or your own server over the public Internet by using SSH. You cannot use this procedure if you
  can only reach the instance or your own server through a virtual private cloud (VPC) or virtual private network (VPN) **and** that VPC or VPN doesn't have access to the public internet.
* If the existing AWS instance is part of an |VPClong| (|VPC|), the VPC must meet |AC9| requirements. 
  For details, see :ref:`Amazon VPC Settings <vpc-settings>`.
* The existing instance or server must have Python installed, and the **version must be 2.7**. To check your version, from your instance's or server's terminal, run the command :command:`python --version`. To install Python 2.7 on your server, see one of the following.

  * :ref:`sample-python-install` in the :title:`Python Sample`.
  * `Download Python <https://www.python.org/downloads/>`_ from the Python website and see `Installing 
    Packages <https://packaging.python.org/installing/>`_ in the :title:`Python Packaging User Guide`.

* The existing instance or server must have Node.js installed, and the **version must be 0.6.16 or later**. To check your version, from your instance's or server's terminal, run the command :command:`node --version`. To install Node.js on your server, see one of the following.

  * :ref:`sample-nodejs-install` in the :title:`Node.js Sample`.
  * `Installing Node.js via package manager <https://nodejs.org/en/download/package-manager/>`_ on the Node.js website.
  * `Node Version Manager <http://nvm.sh>`_ on GitHub.

* The directory that you want |AC9| to start from after login on the existing instance or server must have its access permissions set to :code:`rwxr-xr-x`. This means read-write-execute permissions for the owner, 
  read-execute permissions for the group, and read-execute permissions for others. For example, if the directory's path is :code:`~`, you can set 
  these permissions on the directory by running the :command:`chmod` command on the instance or server, as follows.

  .. code-block:: sh

     sudo chmod u=rwx,g=rx,o=rx ~

Create the |envsshtitle|
------------------------

#. Make sure you completed the preceding prerequisites. 
#. Sign in to the |AC9| console, at |AC9Console_link|.
#. After you sign in to the |AC9| console, in the top navigation bar, choose an AWS Region to create the |env| in. For a list of available AWS Regions, see 
   :aws-gen-ref:`AWS Cloud9 <rande.html#cloud9_region>` in the |AWS-gr|.

   .. image:: images/console-region.png
      :alt: AWS Region selector in the AWS Cloud9 console

#. If a welcome page is displayed, for :guilabel:`New AWS Cloud9 environment`, choose :guilabel:`Create environment`.
   Otherwise, choose :guilabel:`Create environment`.

   .. image:: images/console-welcome-new-env.png
      :alt: Choosing the Next step button if welcome page is displayed

   Or: 
   
   .. image:: images/console-new-env.png
      :alt: Choosing the Create environment button if welcome page is not displayed

#. On the :guilabel:`Name environment` page, for :guilabel:`Name`, type a name for your |env|.
#. To add a description to your |env|, type it in :guilabel:`Description`.
#. Choose :guilabel:`Next step`.
#. For :guilabel:`Environment type:`, choose :guilabel:`Connect and run in remote server (SSH)`.
#. Choose :guilabel:`Copy key to clipboard`. (This is between :guilabel:`View public SSH key` and :guilabel:`Advanced settings`.) 
   Paste the public SSH key value that was copied into the :file:`~/.ssh/authorized_keys` file on the existing instance or server.

   .. note:: To see the public SSH key value that was copied, expand :guilabel:`View public SSH key`.

#. After you paste the public SSH key value, back on the :guilabel:`Configure settings` page in the |AC9| console, 
   for :guilabel:`User`, type the login name you use for the instance or server. 
   For example, for an |EC2| instance running Amazon Linux, it might be :code:`ec2-user`. For another type of server, it might be :code:`root`.
#. For :guilabel:`Host`, type the public IP address (preferred) or the hostname of the instance or server.
#. For :guilabel:`Port`, type the port that you want |AC9| to use to try to connect to the instance or server, or leave the default port.
#. To specify the path to the directory on the instance or server that you want |AC9| to start from after login, which you identified earlier in this procedure's prerequisites, expand :guilabel:`Advanced settings`, 
   and then type the path in :guilabel:`Environment path`. If you leave this blank, |AC9| uses the directory that your instance or server typically starts with after login. This is usually a home or default directory.
#. To specify the path to the Node.js binary on the instance or server, expand 
   :guilabel:`Advanced settings`, and then type the path in :guilabel:`Node.js binary path`. 
   To get the path, you can run the command :command:`which node` (or 
   :command:`nvm which node` if you're using nvm) on your instance or server. 
   For example, the path might be :code:`/usr/bin/node`. 
   If you leave this blank, |AC9| will try to guess where the Node.js binary is when it tries to connect.
#. To specify a jump host that the instance or server uses, expand :guilabel:`Advanced settings`, and then type information about the jump host 
   in :guilabel:`SSH jump host`, using the format :code:`USER_NAME@HOSTNAME:PORT_NUMBER` (for example, 
   :code:`ec2-user@:ip-192-0-2-0:22`)

   The jump host must meet the following requirements.

   * It must be reachable over the public Internet using SSH.
   * It must allow inbound access by any IP address over the specified port.
   * The public SSH key value that was copied into the :file:`~/.ssh/authorized_keys` file on the existing instance or server must also be copied into the :file:`~/.ssh/authorized_keys` file on the jump host.

#. Choose :guilabel:`Next step`.
#. On the :guilabel:`Review` page, choose :guilabel:`Create environment`. Wait while |AC9| creates your |env|. 
   This can take several minutes.

   After |AC9| creates the |env|, it displays the |AC9IDE| for the |env|, and the :guilabel:`AWS Cloud9 installer` dialog box displays. 
   Choose :guilabel:`Next` on each of these confirmation pages to complete the |env| setup process.

If |AC9| doesn't display the |IDE| after at least five minutes, there might be a problem with your web browser, your AWS access permissions, the instance, or the associated
network. For possible fixes, see :ref:`troubleshooting-env-loading` in *Troubleshooting*.




