---

title: 'Add Gateways to the Process'
weight: 40

menu:
  main:
    name: "Make it dynamic"
    parent: "get-started-language-agnostic"
    identifier: "get-started-language-agnostic-gateway"
    pre: "Learn the basics of handling the Camunda Modeler and learn how to model and configure a fully executable process."

---

In this section you learn how to make your process more dynamic by using BPMN 2.0 *Exclusive Gateways*.

# Add two Gateways
We want to modify our process so that we can make it morde dynamic.

To do so, open the process in the Camunda Modeler.

Next, from its context menu, select the gateway shape (diamond) and drag it to a good position between the Start Event and the Service Task. Move down the User Task and add another Gateway after it. Now also adjust the Sequence Flows so the model looks like this.
{{< img src="../img/modeler-gateway1.png" >}}

Now also name the new elements correctly:
{{< img src="../img/modeler-gateway2.png" >}}

# Configure the Gateways

Next, Open the properties view and select the `<1000 €` Sequence Flow after the Gateway on the canvas. This updates the selection in the properties view.
Scroll to the property named `Condition Type` and change it to `Expression`. Then type `${amount<1000}` as the Expression.
We are using the Java Unified Expression Language to evaluate the Gateway. You can also do it in another way, see.

{{< img src="../img/modeler-gateway3.png" >}}

Now, go ahead and change the Expressions for the other Sequence Flows, too.

For the `>=1000 €` Sequence Flow we should use the Expression `${amount>=1000}`:
{{< img src="../img/modeler-gateway4.png" >}}


For the `Yes` Sequence Flow we should use the Expression `${approved}`:
{{< img src="../img/modeler-gateway5.png" >}}

For the `No` Sequence Flow we should use the Expression `${!approved}`:
{{< img src="../img/modeler-gateway6.png" >}}

# Deploy the Process

Use the `Deploy` Button in the Camunda Modeler for deploying the updated process to Camunda.

# Work on the Task

Go to Tasklist ([http://localhost:8080/camunda/app/tasklist](http://localhost:8080/camunda/app/tasklist)) and log in with the user credentials "demo / demo".
Click on the {{< glyphicon name="list-alt" text=" Start process" >}} button to start a process instance. This opens a dialog where you can select *Payment Retrieval* from the list. Now you can set variables for the process instance using a generic form.

{{< img src="../img/start-form-generic.png" >}}

The generic form can be used whenever you have not added a dedicated form for a User Task or a Start Event.
Click on the *Add a variable* button to get a new row. Fill in the form as shown in the screenshot. When you are done, click *Start*.


Now you see the *Approve Payment* task in your Tasklist. Select the task and click on the *Diagram* tab. This displays the process diagram highlighting the User Task that is waiting for you to work on it.

{{< img src="../img/diagram.png" >}}

To work on the task, select the *Form* tab. Because we have defined the variables in the Form Tab in the Camunda Modeler, the Tasklist has automatically generated form fields for us.

{{< img src="../img/task-form-generated.png" >}}

{{< note title="Next Step" class="info" >}}
Seems like you are ready for Decision Automation. Let's have a look how you can [add Business Rules to your Process](xx).
{{< /note >}}

{{< get-tag repo="camunda-get-started-language-agnostic" tag="1-Executable-Model" >}}
