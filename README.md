# machine-controller-manager-provider-sampleprovider
Out of tree (gRPC based) implementation for `SampleProvider` as a new provider.

## About
- This is a sample repository that provides the blueprint required to implement a new (hyperscale) provider. We call the new provider as `SampleProvider` for our ease.
- Each provider (actuator/driver) is a gRPC server and implements the services defined at [machine-spec](https://github.com/gardener/machine-spec).

## Fundamental Design Principles:
Following are the basic principles kept in mind while developing the external driver.
* Communication between external driver and machine-controller is achieved using gRPC mechanism.
* External driver behaves as gRPC-server and machine-controller behaves as gRPC client.
* Cloud-provider specific contract should be scoped under `ProviderSpec` field. `ProviderSpec` field is expected to be raw-bytes at machine-controller-side. External driver should have pre-defined typed-apis to parse the `ProviderSpec` to make necessary CP specific calls.
* External drivers do not need to communicate with kubernetes api-server.
    * Kubeconfig may not be available to external-drivers.

## Support for a new provider
- Steps to be followed while implementing a new provider are mentioned [here](https://github.com/gardener/machine-controller-manager/blob/master/docs/development/new_cp_support.md)