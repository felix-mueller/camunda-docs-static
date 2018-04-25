---

title: 'Deploy the Process'
weight: 30

menu:
  main:
    name: "Deploy"
    parent: "get-started-language-agnostic"
    identifier: "get-started-language-agnostic-deploy"
    pre: "Deploy the Process to Camunda. Test the BPMN 2.0 Process with Tasklist and Cockpit."

---

The next step consists of deploying the Process and starting a new instance using the Camunda Tasklist.

# Use the Camunda Modeler for Deploying the Process

In order to deploy the Process click on the deploy button in the Camunda Modeler, then give it a Deployment Name "Loan Approval" and hit the Deploy button.
{{< img src="../img/modeler-deploy1.png" >}}
{{< img src="../img/modeler-deploy2.png" >}}
You should see a success message in the Camunda Modeler:
{{< img src="../img/modeler-deploy3.png" >}}

# Verify the Deployment with Cockpit

Now use Cockpit to check if the process is successfully deployed. Go to [http://localhost:8080/camunda/app/cockpit](http://localhost:8080/camunda/app/cockpit). Log in with demo / demo. Your process *Loan Approval* is visible on the dashboard.

{{< img src="../img/cockpit-loan-approval.png" >}}


# Start a Process Instance

Next, go to Camunda Tasklist ([http://localhost:8080/camunda/app/tasklist](http://localhost:8080/camunda/app/tasklist)). Click on the {{< glyphicon name="list-alt" text=" Start process" >}} button to start a process instance. This opens a dialog where you can select *Loan Approval* from the list. Now you can set variables for the process instance using a generic form.

{{< img src="../img/start-form-generic.png" >}}

The generic form can be used whenever you have not added a dedicated form for a User Task or a Start Event.
Click on the *Add a variable* button to get a new row. Fill in the form as shown in the screenshot. When you are done, click *Start*.

If you now go back to [Camunda Cockpit](http://localhost:8080/camunda/app/cockpit), you see the newly created process instance that is waiting in the User Task.

# Configure Process Start Authorizations

To allow the user *john* to see the process definition *Loan Approval*, you have to go to Camunda Admin ([http://localhost:8080/camunda/app/admin/default/#/authorization?resource=6](http://localhost:8080/camunda/app/admin/default/#/authorization?resource=6)). Next, click on the button *Create new authorization* to add a new authorization on the resource *process definition*. Now you can give the user *john* all permissions on process definition *approve-loan*. When you are done, submit the new authorization.

{{< img src="../img/create-process-definition-authorization.png" >}}

Now create a second authorization for the *process instance* resource. Set the permission to *CREATE*.

{{< img src="../img/create-process-instance-authorization.png" >}}

For further details about authorizations and how to manage them, please read the following sections in the user guide: [Authorization Service](/manual/latest/user-guide/process-engine/authorization-service) and [Authorization Management](/manual/latest/webapps/admin/authorization-management).


# Work on the Task

Log out of Admin. Go to Tasklist ([http://localhost:8080/camunda/app/tasklist](http://localhost:8080/camunda/app/tasklist)) and log back in with the user credentials "john / john". Now you see the *Approve Loan* task in your Tasklist. Select the task and click on the *Diagram* tab. This displays the process diagram highlighting the User Task that is waiting for you to work on it.

{{< img src="../img/diagram.png" >}}

To work on the task, select the *Form* tab. Again, there is no task form associated with the process. Click on *Load Variables*. This displays the variables you have put in in the first step.

{{< img src="../img/task-form-generic.png" >}}
