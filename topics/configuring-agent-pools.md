[//]: # (title: Configuring Agent Pools)
[//]: # (auxiliary-id: Configuring Agent Pools;Agent Pools;Agent Pool)

Instead of having one common set of [build agents](build-agent.md), you can break them into separate groups called _agent pools_. A pool is a named set of agents to which you can assign projects.
* An agent can belong to _one pool only_.
* A project can use _multiple pools_ for its builds.

The number of agents authorized by the TeamCity server is limited by the number of [agent licenses](licensing-policy.md#Number+of+Agents). By default, all newly authorized agents are included into the _Default pool_.
{product="tc"}

The number of agents authorized by the TeamCity server is limited by the number of agent licenses. By default, all newly authorized agents are included into the _Default pool_.
{product="tcc"}

With the help of agent pools you can bind specific agents to specific projects. Project builds can be run only on build agents from the pools assigned to the project. Besides, using agent pools makes it easier to monitor the required agents' capacity.

Using agent pools allows:
* Binding specific agents to specific projects: project builds can be run only on build agents from the pools assigned to the project.
* Filtering the build queue by pools.
* Use grouping by pool on the [Agent Matrix and Agent Statistics](viewing-agents-workload.md) pages.
* Monitoring the required agents' capacity.

## Required Permissions

To be able to add/remove pools and set maximum number of agents in the pool, you need to have the "_Manage agent pools_" permission granted to the System Administrator and Agent Manager [roles](managing-roles-and-permissions.md) in the default TeamCity [per-project authorization mode](managing-roles-and-permissions.md#Per-Project+Authorization+Mode).

Assigning and unassigning projects and agents to/from pools is restricted by the "_Change agent pools associated with project_" permission, which by default is a part of the Project Administrator role. Users can perform the operations on the pool only if they have the "_Change agent pools associated with project_" permission for _all projects_ associated with _all pools_ affected by the operation.

See also related [agent management permissions](managing-roles-and-permissions.md#Project-level+Agent+Management+Permissions).

## Managing Agent Pools

You can manage build agents on the __Agents__ page, a link to which is located in the UI header. If you are using the classic UI mode, note that it has a different navigation system than described in this article: pools are managed on the __Agents | Pools__ tab.  

The _Agents_ sidebar allows navigating between the existing agent pools and shows the agent statuses in real time.

To create a new pool, click __+__ in the sidebar and enter its name.  
By default, a pool contains an unlimited number of agents. You can set a maximum number of agents in the pool (not applicable to the _Default_ pool). If the maximum number of agents is reached, TeamСity will not allow adding any new agents to this pool. This includes moving agents from other pools and automatic authorization of cloud agents. New cloud agents will not start if the target pool is full.

To see the details of a certain pool or its nested [agent](viewing-build-agent-details.md), click its name in the sidebar.

### Agents Tab

To populate a pool with agents, click __Assign agents__ on the __Agents__ tab and select the required agents from the list. Since an agent can belong to only one pool, assigning it to a pool will remove it from its previous pool. If TeamCity detects that this action might cause compatibility problems, it will show a respective warning. Removing an agent from a custom pool will return it to the _Default_ pool.

To assign a cloud agent to a pool, you need to configure it in the cloud image details of the [agent cloud profile](agent-cloud-profile.md). Note that agents from all cloud profiles of the current project are automatically combined into a _[project pool](agent-cloud-profile.md#Adding+Agent+Image)_.  
Only cloud agent images configured in the `<Root>` project can be moved using __Assign agents__.
{product="tc"}

### Projects Tab

To bind certain projects to an agent pool, open the __Projects__ tab, click __Assign projects__, and select the required projects. You can choose to detach them from their previous pools, if necessary.  
After you save the settings, TeamCity will only be running builds of these projects on the agents from the current pool.

<seealso>
        <category ref="concepts">
            <a href="build-agent.md">Build Agent</a>
            <a href="working-with-build-queue.md">Working with Build Queue</a>
            <a href="agent-requirements.md">Agent Requirements</a>
        </category>
        <category ref="admin-guide">
            <a href="viewing-agents-workload.md">Viewing Agents Workload</a>
            <a href="agent-cloud-profile.md" product="tc">Agent Cloud Profile</a>
        </category>
</seealso>
