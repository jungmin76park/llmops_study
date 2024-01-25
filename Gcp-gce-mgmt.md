To manage Google Cloud Platform (GCP) virtual machines (VMs) using Python, you need to use the Google Cloud Python client libraries. Below are examples of how to perform the tasks you've listed. Before running these scripts, make sure you have set up Google Cloud SDK and authenticated your environment.

1. **Get VM List with Specified Label:**
   To list VMs with a specific label, you can use the `compute_v1` module from Google Cloud's Python client library.

   First, install the required library if you haven't already:
   ```
   pip install google-cloud-compute
   ```

   Then, you can use the following code:
   ```python
   from google.cloud import compute_v1

   def list_instances_with_label(project_id, zone, label_key, label_value):
       instance_client = compute_v1.InstancesClient()
       request = compute_v1.AggregatedListInstancesRequest(project=project_id)
       agg_list = instance_client.aggregated_list(request=request)

       for zone, response in agg_list:
           for instance in response.instances:
               labels = instance.labels
               if labels and labels.get(label_key) == label_value:
                   print(f"Instance name: {instance.name}")

   # Usage
   project_id = "your-project-id"
   zone = "your-zone"
   label_key = "your-label-key"
   label_value = "your-label-value"
   list_instances_with_label(project_id, zone, label_key, label_value)
   ```

2. **Check VM State:**
   You can check the state of a VM by retrieving its status.

   ```python
   def check_instance_state(project_id, zone, instance_name):
       instance_client = compute_v1.InstancesClient()
       instance = instance_client.get(project=project_id, zone=zone, instance=instance_name)
       return instance.status

   # Usage
   project_id = "your-project-id"
   zone = "your-zone"
   instance_name = "your-instance-name"
   state = check_instance_state(project_id, zone, instance_name)
   print(f"Instance state: {state}")
   ```

3. **Start VM:**
   To start a stopped VM, you can use the `start` method.

   ```python
   def start_instance(project_id, zone, instance_name):
       instance_client = compute_v1.InstancesClient()
       operation = instance_client.start(project=project_id, zone=zone, instance=instance_name)
       return operation

   # Usage
   project_id = "your-project-id"
   zone = "your-zone"
   instance_name = "your-instance-name"
   start_instance(project_id, zone, instance_name)
   ```

4. **Stop VM:**
   To stop a running VM, you can use the `stop` method.

   ```python
   def stop_instance(project_id, zone, instance_name):
       instance_client = compute_v1.InstancesClient()
       operation = instance_client.stop(project=project_id, zone=zone, instance=instance_name)
       return operation

   # Usage
   project_id = "your-project-id"
   zone = "your-zone"
   instance_name = "your-instance-name"
   stop_instance(project_id, zone, instance_name)
   ```

Remember to replace `"your-project-id"`, `"your-zone"`, `"your-instance-name"`, `"your-label-key"`, and `"your-label-value"` with your actual GCP project ID, zone, instance name, label key, and label value. Also, ensure that your environment is correctly set up with the appropriate permissions and credentials to interact with the GCP Compute Engine API.
