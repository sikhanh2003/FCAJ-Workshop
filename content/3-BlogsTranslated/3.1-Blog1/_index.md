---
title: "Blog 1"
date: "2024-01-01"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AWS Big Data Blog

## Introducing Apache Airflow 3 on Amazon MWAA: New features and capabilities

by Anurag Srivastava, Ankit Sahu, Kamen Sharlandjiev, Sriharsh Adari, Mohammad Sabeel, and Satya Chikkala on 01 OCT 2025 in Advanced (300), Amazon Managed Workflows for Apache Airflow (Amazon MWAA), Announcements Permalink Comments Share

Today, Amazon Web Services (AWS) announced the general availability of Apache Airflow 3 on Amazon Managed Workflows for Apache Airflow (Amazon MWAA). This release transforms how organizations use Apache Airflow to orchestrate data pipelines and business processes in the cloud, bringing enhanced security, improved performance, and modern workflow orchestration capabilities to Amazon MWAA customers.

Amazon MWAA introduces Airflow 3 features that modernize workflow management for AWS customers. Following the April 2025 release of Airflow 3 by the Apache community, AWS has incorporated these capabilities into Amazon MWAA. Airflow now features a completely redesigned, intuitive UI that simplifies workflow orchestration for users across experience levels. With the Task Execution Interface (Task API), tasks can run both within Airflow and as standalone Python scripts, improving code portability and testing. Scheduler-managed Backfill moves operations from the CLI to the scheduler, providing centralized control and visibility through the Airflow UI. CLI security improvements replace direct database access with API calls, maintaining consistent security across interfaces. Airflow now supports event-driven workflows, enabling triggers from AWS services and external sources. Amazon MWAA also adds support for Python 3.12, bringing the latest language capabilities to workflow development.

This post explores the features of Airflow 3 on Amazon MWAA and outlines enhancements that improve your workflow orchestration capabilities. The service maintains the Amazon MWAA pay-as-you-go pricing model with no upfront commitments. You can begin immediately by visiting the Amazon MWAA console, launching new Apache Airflow environments through the AWS Management Console, AWS Command Line Interface (AWS CLI), AWS CloudFormation, or AWS SDK within minutes.

### Architectural advancements in Airflow 3 on Amazon MWAA

Airflow 3 on Amazon MWAA introduces significant architectural improvements that enhance security, performance, and flexibility. These advancements create a more robust foundation for workflow orchestration while maintaining backward compatibility with existing workflows.

#### Enhanced security

Amazon MWAA with Airflow 3 changes the security model by making component isolation a standard practice rather than optional. In Airflow 2, the DAG processor (the component that parses and processes DAG files) runs within the scheduler process by default, but can optionally be separated into its own process for better scalability and security isolation. Airflow 3 makes this separation standard, maintaining consistent security practices across deployments.

#### API server and Task API

Building on this security foundation, a new API server component is introduced in Amazon MWAA with Airflow 3, which serves as an intermediary between task instances and the Airflow metadata database. This change improves your workflows’ security posture by minimizing direct access to the Airflow metadata database from tasks. Tasks now operate with least privilege database access, reducing the risk of one task affecting others and improving overall system stability through fewer direct database connections.

The standardized communication through well-defined API endpoints creates a foundation for more secure, scalable, and flexible workflow orchestration. The Task Execution Interface (Task API) helps tasks run both within Airflow and as standalone Python scripts, improving code portability and testing capabilities.

#### From data-aware to event-driven scheduling

Airflow’s evolution toward event-driven scheduling began with the introduction of data-aware scheduling in Airflow 2.4, so DAGs could be triggered based on data availability rather than time schedules alone. Amazon MWAA with Airflow 3 builds on this foundation through a transition that includes the renaming of datasets to assets and introduces advanced capabilities, including asset partitions, external event integration, and asset-centric workflow design.

The transition from datasets to assets represents more than a simple rename. A data asset is a collection of logically related data that can represent diverse data products, including database tables, persisted ML models, embedded dashboards, or directories containing files.

Amazon MWAA with Airflow 3 introduces a new asset-centric syntax that represents an important shift in how workflows can be designed. The @asset decorator helps developers put data assets at the center of their workflow design, creating more intuitive asset-driven pipelines.

The following code is an example of asset-aware DAG scheduling:

```python
from airflow.sdk import DAG, Asset
from airflow.providers.standard.operators.python import PythonOperator

# Define the asset
customer_data_asset = Asset(name="customer_data", uri="s3://my-bucket/customer-data.csv")

def process_customer_data():
    """Process customer data..."""
    # Implementation here

# Create the DAG and task
with DAG(dag_id="process_customer_data", schedule="@daily"):
    PythonOperator(
        task_id="process_data", 
        outlets=[customer_data_asset], 
        python_callable=process_customer_data
    )
```

The following code shows an asset-centric approach with the @asset decorator:

```python
from airflow.sdk import asset

@asset(uri="s3://my-bucket/customer-data.csv", schedule="@daily")
def customer_data():
    """Process customer data..."""
    # Implementation here
```

The @asset decorator automatically creates an asset with the function name, a DAG with the same identifier, and a task that produces the asset. This reduces code complexity and facilitates automatic DAG creation, where each asset becomes a self-contained workflow unit.

#### External event-driven scheduling with Asset Watchers

A significant advancement in Amazon MWAA with Airflow 3 is the introduction of Asset Watchers, which help Airflow react to events happening outside of the Airflow system itself. Whereas previous versions supported internal cross-DAG dependencies, Asset Watchers extend this capability to external data systems and message queues through the AssetWatcher class.

Amazon MWAA with Airflow 3 includes support for Amazon Simple Queue Service (Amazon SQS) through Asset Watchers. This allows your workflows to be triggered by external messages and facilitates more event-driven scheduling. Airflow now supports event-driven workflows, enabling triggers from AWS services and external sources. Asset Watchers monitor external systems asynchronously and trigger workflow execution when specific events occur, enabling workflows to respond to business events, data updates, or system notifications without the overhead of traditional sensor-based polling mechanisms.

#### Modern React-based UI

Amazon MWAA with Airflow 3 features a completely redesigned, intuitive UI built with React and FastAPI that simplifies workflow orchestration for users across experience levels. The new interface provides more intuitive navigation and workflow visualization, with an enhanced grid view that offers better visibility into task status and history. Users will appreciate the addition of dark mode support, which reduces eye strain during extended use, and the overall faster performance that’s especially noticeable when working with large DAGs.

The new UI maintains familiar workflows while providing a more modern and efficient experience for DAG management and monitoring, making daily operations more productive for both developers and operators. The legacy UI has been completely removed, offering a cleaner, more consistent experience across the system. The foundation for the new UI is built on REST APIs and a set of internal APIs for UI operations, both of which are now based on FastAPI, creating a more cohesive and secure architecture for both programmatic access and UI operations.

#### Scheduler optimizations

Amazon MWAA with Airflow 3’s enhanced scheduler delivers performance improvements for task execution and workflow management. The redesigned scheduling engine processes tasks more efficiently, reducing the time between task submissions and executions. This optimization benefits data pipeline operations that require rapid task processing and timely workflow completion.

The scheduler now manages computing resources more effectively, enabling stable performance even as workloads scale. When running multiple DAGs simultaneously, the improved resource allocation system helps prevent bottlenecks and maintains consistent execution speeds. This advancement is particularly useful for organizations running complex workflows with varying resource requirements. The new scheduler also handles concurrent operations with increased precision, so teams can run multiple DAG instances simultaneously while maintaining system stability and predictable performance.

#### Enhanced scheduler backfill operations

Scheduler-managed backfill (the process of running DAGs for historical dates) moves operations from the CLI to the scheduler, providing centralized control and visibility through the Airflow UI. Amazon MWAA with Airflow 3 delivers important upgrades to the scheduler’s backfill capabilities, helping data teams process historical data more efficiently. The backfill process has been optimized for better performance, reducing the database load during these operations and making sure backfills can be completed more quickly, minimizing the impact on near real-time workflow execution.

Amazon MWAA with Airflow 3 also improves the management of backfill operations, with the scheduler providing better isolation between backfill jobs and supporting more efficient processing of historical datasets. Operators now have better monitoring tools to track the progress and status of their backfill jobs, resulting in more effective management of these critical data processing tasks.

### Developer-focused improvements

Airflow 3 on Amazon MWAA delivers several enhancements designed to improve the developer experience, from simplified task definition to better workflow management capabilities.

#### Task SDK

The Task SDK provides a more intuitive way to define tasks and DAGs:

```python
# Example using the Task SDK
from airflow.sdk import dag, task
from datetime import datetime

@dag(
    start_date=datetime(2023, 1, 1),
    schedule="@daily",
    catchup=False
)
def modern_etl_workflow():
    
    @task
    def extract():
        # Extract data from source
        return {"data": [1, 2, 3, 4, 5]}
    
    @task
    def transform(input_data):
        # Transform the data
        return [x * 10 for x in input_data]
    
    @task
    def load(transformed_data):
        # Load data to destination
        print(f"Loading data: {transformed_data}")
    
    # Define the workflow
    extracted_data = extract()
    transformed_data = transform(extracted_data["data"])
    load(transformed_data)

# Instantiate the DAG
etl_dag = modern_etl_workflow()
```

This approach offers more intuitive data flow between tasks, better integrated development environment (IDE) support with improved type hinting, and more straightforward unit testing of task logic. The result is cleaner, more maintainable code that better represents the actual data flow of your pipelines. Teams adopting this pattern often find their DAGs become more readable and simpler to maintain over time, especially as workflows grow in complexity.

#### DAG versioning

Amazon MWAA with Airflow 3 includes basic DAG versioning capabilities that come by default with Airflow 3. Each time a DAG is modified and deployed, Airflow serializes and stores the DAG definition to preserve history. This automatic version tracking minimizes the need for manual record-keeping and ensures every modification is documented.

Through the Airflow UI, teams can access and review the history of their DAGs. This visual representation shows version numbers (v1, v2, v3, etc.) and helps teams understand how their workflows have evolved over time.

The DAG versioning supported in Amazon MWAA provides the capability to see different DAG versions that were run in the Airflow UI, offering improved workflow visibility and enhanced collaboration for data engineering teams managing complex, evolving data pipelines.

#### Python 3.12 support

Amazon MWAA adds support for Python 3.12, bringing the latest language capabilities to workflow development. This upgrade provides access to the latest Python language improvements, performance enhancements, and library updates, keeping your data pipelines modern and efficient.

### Features not currently supported in Amazon MWAA

Although we are launching most of the Airflow 3 features on Amazon MWAA in this release, some features are not supported at this time:

* Replace Flask AppBuilder (AIP-79) – Full replacement capabilities

* Edge Executor and task isolations (AIP-69) – Full remote execution capabilities

* Multi-language support (AIP-72) – Support for languages other than Python

We plan to support these features in subsequent versions of Airflow on Amazon MWAA.

### Conclusion

Airflow 3 on Amazon MWAA delivers enhanced workflow automation capabilities. The architectural improvements, enhanced security model, and developer-friendly features provide a solid foundation for building more reliable and maintainable data pipelines.The introduction of Asset Watchers changes how workflows can respond to external events, enabling truly event-driven scheduling. This capability, combined with the new asset-centric workflow design, makes Airflow 3 a more powerful and flexible orchestration service.

The scheduler optimizations deliver performance improvements for task execution and workflow management, and the enhanced backfill capabilities make historical data processing more efficient. The DAG versioning system improves workflow stability and collaboration, and Python 3.12 support keeps your data pipelines modern and efficient.

Organizations can now take advantage of these new features and improvements in Airflow 3 on Amazon MWAA to enhance their workflow orchestration capabilities. To get started, visit the Amazon MWAA product page.
