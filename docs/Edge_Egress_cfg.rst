Configure Edge Data Store Egress
================================

You use the IQiEdgeEgressService instance to configure various aspects of the Egress feature of Edge Data Store. 
The sections that follow show how to specify and work with egress targets. You can configure the destination to 
which your Edge Data Store server will transfer data. Possible target products are:

•	OSIsoft Cloud Services
•	PI System

Creating a new EgressTarget
---------------------------

Use the ``CreateTargetAsync`` method to add a new EgressTarget to an Edge Data Store server, as shown here:

::

  egressService.CreateTargetAsync(targetId, description, targetType);

•	``targetId`` is a unique id you assign to this EgressTarget instance
•	``description`` is a meaningful description for this EgressTarget instance
•	``targetType`` must be a value of the ``Models.OmfEgress.EgressTarget.EgressTargetType`` enum specifying what the destination product is (either OCS or PI)

Starting the egress for an existing EgressTarget
------------------------------------------------

Use the ``StartTargetAsync`` method to begin egressing (sending) events to the target destination:

::

  egressService.StartTargetAsync(targetId);

•	``targetId`` is the unique id for the EgressTarget to start

Stopping the egress for an existing EgressTarget
------------------------------------------------

Use the ``StopTargetAsync`` method to halt the egress of events to the target destination:

::

  egressService.StopTargetAsync(targetId);

•	``targetId`` is the unique id for the EgressTarget to stop


Determine whether an existing EgressTarget is running
-----------------------------------------------------

To determine whether an existing EgressTarget is currently sending data to the target destination, 
use the ``PingTargetAsync`` method, as shown here:

::

  egressService.PingTargetAsync(targetId);

•	``targetId`` is a unique id you assigned to this EgressTarget instance

Deleting an existing EgressTarget
---------------------------------

To delete an existing EgressTarget, use the DeleteTargetAsync method, as shown here:

::

  egressService.DeleteTargetAsync(targetId);

•	``targetId`` is a unique id you assigned to this EgressTarget instance 

Updating an existing EgressTarget
---------------------------------

To update an existing EgressTarget, use the ``UpdateTargetAsync`` method:

::

  egressService.UpdateTargetAsync(targetId, newTargetId, newDescription);

*	``targetId`` is the Id of the existing EgressTarget instance
*	``newTargetId`` is a new Id to assign to the EgressTarget
*	``newDescription`` is a new description for the EgressTarget



Retrieving list of existing EgressTargets
-----------------------------------------

To retrieve a list of existing EgressTargets, use the ``GetTargetsAsync`` method:

::

  egressService.GetTargetsAsync();


