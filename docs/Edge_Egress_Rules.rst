Edge Data Store egress rules
============================

EgressRules allows you to configure exactly which types, streams, and event data are transferred from the Edge Data 
Store server to other products within the OSIsoft ecosystem.

By default, when an EgressTarget is configured, all types, streams, and event data are transferred to the target system. 
You can configure filters to specify which of these items are transferred to the target system. After EgressRules are 
attached to an EgressTarget, only types, streams, and events that match the specified rules are transferred.

Configuring EgressRules
-----------------------

After an EgressTarget has been configured, EgressRules may be attached to them. To configure an EgressRule 
and attach it to an EgressTarget, instantiate an EgressRule object and then add it to an egress target with 
the ``CreateRuleAsync`` method, as shown here:

::

  Instantiating an EgressRule
  var rule = new EgressRule()
  {
      Id = "EgressTankTemperatureData",
      Name = "Dangerous tank temperature",
      Description = "Egress if tank temperature exceeds 95 Celsius",
      StreamFilterId = "TankTemperature*",
      StreamFilterTypeId = “TankTemperatureType”,
      EventFilter = "Temperature gt 95",
  };
  
•	``Id`` is the unique id you assign to the EgressRule
•	``Name`` is name for the EgressRule
•	``Description`` is a description for the EgressRule
•	``StreamFilterId`` is a regex for the Id of the stream to filter.
•	``StreamFilterTypeId`` is a regex the type of the stream to filter.
•	``EventFilter`` is a filter expression that dictates what events can be egressed. For assistance writing 
    filter expressions for the EventFilter property, consult OCS documentation: http://qi-docs.readthedocs.io/en/latest/Filter%20Expressions.html
    
Creating a new EgressRule
-------------------------

Use the ``CreateRuleAsync`` method to add a rule to the specified egress target, as shown here:

::

  egressService.CreateRuleAsync(targetId, rule);

•	``targetId`` is the unique id of EgressTarget instance to which an EgressRule should be added
•	``rule`` is an EgressRule instance to add

Deleting an existing EgressRule
-------------------------------

Use the ``DeleteRuleAsync`` method to delete an existing EgressRule from the specified egress target:

::

  egressService.DeleteRuleAsync(targetId, ruleId);

•	``targetId`` is a unique id for an EgressTarget instance containing the EgressRule to delete
•	``ruleId`` is the unique id of the EgressRule to delete from the egress target

Updating an existing EgressRule
-------------------------------

Use the ``UpdateRuleAsync`` method to update an existing EgressRule of a specified egress target:

::

  egressService.UpdateRuleAsync(targetId, ruleId, updatedRule);

•	``targetId`` is the unique id of the EgressTarget instance for which an EgressRule should be updated
•	``ruleId`` is the unique id of the EgressRule to update from the egress target
•	``updatedRule`` is an EgressRule instance with the updated properties

Listing existing EgressRules
----------------------------

Use the ``GetRulesAsync`` method to retrieve a list of EgressRule objects for the specified egress target:

::

  egressService.GetRulesAsync(targetId);

•	``targetId`` is the unique id for an EgressTarget instance containing the rules to return



