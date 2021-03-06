## CSI Controller driver compliance

Following matrix shows lvm-localpv controller driver capabilities.

| Capability | Description | Status | Comment |
| -------------------------------- | -------------- | ------------ | ------------ |
| CREATE_DELETE_VOLUME | This capability indicates that the driver supports dynamic volume provisioning and deprovisioning. | Implemented |  |
| PUBLISH_UNPUBLISH_VOLUME | This capability indicates the driver implements operations that correspond to the Kubernetes volume attach/detach operations. | Not applicable | This functionality is not required for LVM CSI driver as this is local volume and available on the node. |
| LIST_VOLUMES |  | Not implemented |  |
| GET_CAPACITY | This capability indicates that the driver supports exposing available capacity of the storage pool from which the controller provisions volumes. | Implemented |  |
| CREATE_DELETE_SNAPSHOT | This capability indicates that the driver supports provisioning volume snapshots and the ability to provision new volumes using those snapshots. | Implemented | Creation and deletion of volume snapshot is implemented but creating a volume using snapshot is not supported. |
| LIST_SNAPSHOTS |  | Not implemented |  |
| CLONE_VOLUME | This capability indicates that the driver supports provisioning a volume from existing volume. | Not implemented |  |
| PUBLISH_READONLY |  This capability indicates that the driver supports ControllerPublishVolume as readonly. | Not applicable | As controller publish is not applicable this is also not applicable. |
| EXPAND_VOLUME | This capability indicates that the driver supports expansion of  existing volume. | Implemented |  |
| LIST_VOLUMES_PUBLISHED_NODES | This capability indicates that the SP adds published_node_ids field in list volume response. | Not implemented |  |
| VOLUME_CONDITION | This capability indicates that the SP adds volume_condition field in get volume response. | Not implemented |  |
| GET_VOLUME |  | Not implemented |  |



## CSI Node driver compliance

Following matrix shows lvm-localpv node driver capabilities.

| Capability | Description | Status | Comment |
| -------------------------------- | -------------- | ------------ | ------------ |
| STAGE_UNSTAGE_VOLUME | This capability indicates that the driver implements functionality to mount/unmount the volume at staging path. | Not applicable | Not required to mount and unmount the volume in staging path for now. |
| GET_VOLUME_STATS |  This capability indicates that the driver supports exposing volume statistics. | Implemented |  |
| EXPAND_VOLUME | This capability indicates that the driver supports expansion of  existing volume. | Implemented |  |
| VOLUME_CONDITION | This capability indicates that the SP adds volume_condition field in get volume response. | Not implemented |  |



## CSI VolumeCapability compliance

Following matrix shows lvm-localpv VolumeCapability.

| Name | Description | Status | Comment |
| -------------------------------- | -------------- | ------------ | ------------ |
| AccesssType Block | Volume can be accessed via the block device API. | Supported |  |
| AccesssType Mount | Volume can be accessed via the filesystem API. | Supported |  |
| AccessMode - SINGLE_NODE_WRITER | Volume can only be published once as read/write on a single node, at any given time. | Supported |  |
| AccessMode - SINGLE_NODE_READER_ONLY | Volume can only be published once as readonly on a single node, at any given time. | Not applicable | This CSI driver is used in k8s and there is no readonly once access mode in k8s. |
| AccessMode - MULTI_NODE_READER_ONLY | Volume can be published as readonly at multiple nodes simultaneously. | Not applicable | LVM volume is available on single node where the disks are attached for VG. |
| AccessMode - MULTI_NODE_SINGLE_WRITER | Volume can be published at multiple nodes simultaneously. Only one of the node can be used as read/write. The rest will be readonly. | Not applicable | LVM volume is available on single node where the disks are attached for VG. |
| AccessMode - MULTI_NODE_MULTI_WRITER | Volume can be published as read/write at multiple nodes simultaneously | Not applicable | LVM volume is available on single node where the disks are attached for VG. |
