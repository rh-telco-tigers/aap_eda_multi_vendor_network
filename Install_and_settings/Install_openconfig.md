# Installing OpenConfig on Arista EOS and Cisco NX-OS

This guide will walk you through the installation and setup of OpenConfig on Arista EOS and Cisco NX-OS devices. OpenConfig is a collaborative initiative to develop a consistent set of network data models for configuring and monitoring network devices.

## Prerequisites

Before proceeding, ensure the following:

- **Access to Arista EOS and Cisco NX-OS devices.**
- **Administrative privileges** on both devices.
- **OpenConfig model files** (you can fetch them from the [OpenConfig GitHub Repository](https://github.com/openconfig/public)).
- **NETCONF, gNMI, or another supported management protocol** configured on your devices.

### Arista EOS Prerequisites
- EOS version 4.18.0 or higher.
- `Management API` must be enabled for NETCONF or gNMI communication.

### Cisco NX-OS Prerequisites
- NX-OS version 9.2(1) or higher.
- NETCONF or gNMI needs to be enabled.

---

## 1. Installation on Arista EOS

### Step 1: Enable Management API (NETCONF or gNMI)

On Arista EOS, ensure the management API is enabled. You can use NETCONF or gNMI.

#### For NETCONF:
1. Log into the device via SSH.
2. Enable NETCONF with the following command:

   ```bash
   switch(config)# management api netconf
   switch(config)# transport ssh
   ```

#### For gNMI:
1. Enable gRPC on the device:

   ```bash
   switch(config)# management api gnmi
   switch(config-gnmi)# transport grpc default
   ```

2. You may also need to enable SSL/TLS support depending on your setup for secure gRPC communication. Ensure that the appropriate certificates are in place on your device for secure gRPC sessions.
3. Test the gNMI connection using an external gNMI client or your automation tool. Confirm that gNMI responses are correct and verify any configurations made using OpenConfig models.

### Step 2: Install OpenConfig Models

1. Download OpenConfig models from [OpenConfig GitHub](https://github.com/openconfig/public).
2. Transfer the models to the Arista device using SCP or another file transfer method.
3. Load the models into the device configuration. Use the following syntax:

   ```bash
   switch(config)# openconfig
   switch(config)# end
   ```

### Step 3: Verify Installation

You can verify that the OpenConfig models are properly installed by checking the YANG models available on the device:

```bash
switch# show management api yang-models
```

---

## 2. Installation on Cisco NX-OS

### Step 1: Enable NETCONF or gNMI

On Cisco NX-OS, you need to enable either NETCONF or gNMI for OpenConfig to function properly.

#### For NETCONF:
1. Enable NETCONF using the following commands:

   ```bash
   feature netconf
   ```

#### For gNMI:
1. Enable gRPC with the following command:

   ```bash
   feature grpc
   grpc gnmi
   grpc tls use-system-certs
   ```

2. You may need to configure the necessary certificates for gRPC if TLS is required by your setup. Test the gNMI connection to ensure proper communication with your automation tool or controller.

### Step 2: Install OpenConfig Models

1. Download the required OpenConfig models from the [OpenConfig GitHub Repository](https://github.com/openconfig/public).
2. Transfer these models to the Cisco NX-OS device using SCP or another secure file transfer method.
3. Load the models into the device configuration:

   ```bash
   terminal (config)# openconfig
   ```

### Step 3: Verify Installation

Check that the OpenConfig models have been loaded successfully with:

```bash
show openconfig models
```

---

## 3. Additional Configuration

### Using NETCONF
Ensure the NETCONF connection is active by testing it with your controller or automation tool.

### Using gNMI
Make sure your gNMI client is correctly configured to connect to the device and test model-based configurations.

---

## 4. Troubleshooting

### Common Issues:
- **Incorrect version:** Ensure your devices are running compatible versions of EOS (4.18.0+) and NX-OS (9.2(1)+).
- **NETCONF/gNMI not enabled:** Ensure that you have enabled the necessary management APIs (NETCONF or gNMI).
- **Model mismatch:** Verify that the correct OpenConfig models are transferred and loaded.

### Logs:
- Use the `show logging` command on both devices to review logs related to OpenConfig and NETCONF/gNMI communications.
