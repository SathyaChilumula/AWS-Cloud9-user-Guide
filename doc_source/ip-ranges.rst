.. Copyright 2010-2018 Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _ip-ranges:

#######################################
Inbound SSH IP Address Ranges for |AC9|
#######################################

.. meta::
    :description:
        Lists the inbound IP address ranges that AWS Cloud9 uses to connect to hosts over SSH.

You can restrict incoming traffic to just the IP address ranges that |AC9| uses to connect over SSH to AWS cloud compute instances (for example |EC2| instances) in an |VPC| or your own servers in your network.

.. note:: For an |envec2| created on or after July 31 2018, you can skip this topic. This is because |AC9| automatically restricts inbound SSH traffic for that |env| to only those IP addresses that are 
   described later in this topic. |AC9| does this by automatically adding a rule to the security group that is associated with the |EC2| instance for the |env|. 
   This rule restricts inbound SSH traffic over port 22 to only those IP addresses for the associated AWS Region.

These IP address ranges are in the :file:`ip-ranges.json` file, as described in :AWS-gr:`AWS IP Address Ranges <aws-ip-ranges>` in the |AWS-gr|.
To find the IP ranges in that file:

* For Windows, using the |TWPlong|, run the following command.

  .. code-block:: powershell

     Get-AWSPublicIpAddressRange -ServiceKey CLOUD9

* For Linux, download the `ip-ranges.json <https://ip-ranges.amazonaws.com/ip-ranges.json>`_ file. Then you can query it by using a tool such as
  :command:`jq`, for example by running the following command. 
  
  .. code-block:: sh 
  
     jq '.prefixes[] | select(.service=="CLOUD9")' < ip-ranges.json

These IP ranges might change occasionally. Whenever there's a change, we send notifications to subscribers of the :code:`AmazonIpSpaceChanged` topic. 
To get these notifications, see :aws-gen-ref:`AWS IP Address Ranges Notifications <aws-ip-ranges.html#subscribe-notifications>` in the |AWS-gr|.

To use these IP address ranges when configuring |envplural| that use AWS cloud compute instances, see :ref:`Amazon VPC Settings <vpc-settings>`. Also, 
if you choose to restrict incoming traffic for |envec2plural|, or for |envsshplural| associated with |EC2| instances running Amazon Linux, be sure to also allow at minimum 
all IP addresses using TCP over ports 32768-61000. For more information, as well as port ranges for other AWS cloud compute instance types, 
see :vpc-user-guide:`Ephemeral Ports <VPC_ACLs.html#VPC_ACLs_Ephemeral_Ports>` in the |VPC-ug|.

To use these IP address ranges when configuring |envsshplural| that use your own network, see your network's documentation or your network administrator.