Kubernetes
==========

.. versionadded:: 1.1


From `Kubernetes.io <http://kubernetes.io>`_:

    Kubernetes is an open-source system for automating deployment, operations,
    and scaling of containerized applications.

Since version 1.1, Mantl ships Kubernetes by default. All you need to do is set
the ``kubeworker_count`` and ``kubeworker_type`` variables in your Terraform
configuration (see the example Terraform configurations for where this variable integrates into the
workflow.)

`kubectl` is installed and configured for the default SSH user on the control
nodes. Please refer to the `Kubernetes getting started documentation
<http://kubernetes.io/docs/hellonode/>`_ for how to use Kubernetes.

To talk to the services launched inside Kubernetes, launch them with the
``NodePort`` service type (`more on what service types are available
<https://aster.is/blog/2016/03/11/the-hamburger-of-kubernetes-service-types/>`_),
then connect on the assigned port on any Kubernetes worker node. Consul service
integration will happen in a future release.

Cloud Provider Integration
--------------------------

As of 1.3, when you install Mantl on an AWS cluster, Kubernetes cloud provider
integration will be enabled by default. Kubernetes will be able to natively
manage some AWS resources (such as ELBs or EBS persistent volumes). If you wish
to disable cloud provider integration, set the variable
``enable_cloud_provider`` to ``false`` when building your cluster.

.. note:: If you are planning on destroying your cluster with terraform, you
          should first use ``kubectl`` or the Kubernetes API to delete your
          Kubernetes-managed AWS resources. Otherwise, it can cause your
          ``terraform destroy`` command to fail.
