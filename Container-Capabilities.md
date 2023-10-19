# Capabilities
- Capabilities provide ability to give a small set of privileges to a thread/ process.
- All privileged actions are categorised into 40 capabilities.
- Purpose of capabilities is to divide root privileges into dustinct privileges.
- By default Docker Runtime start with below capabilities:
cap_chown, cap_dac_override, cap_fowner, cap_fsetid, cap_kill, cap_setgid, cap_setuid, cap_setpcap, cap_net_bind_service, cap_net_raw, cap_sys_chroot, cap_mknod, cap_audit_write, cap_setfcap
- Below is the image showing privileges breakdown in container:</br>
![Privileges_Breakdown](https://github.com/Vamckis/Container-Security/assets/71128825/88e85dc3-a8f8-4b2e-af35-5f7e387500fe)

### Capabilities Commands
- With Docker Runtime:
``` docker run --cap-add=<CAP> -it <Image name> ```
``` docker run --cap-add ALL -it <Image name> ```
``` docker run --cap-drop=<CAP> -it <Image name> ```
``` docker run --cap-add ALL -it <Image name> ```
- With Kubernetes, we can add/drop in Security Context</br>
![image](https://github.com/Vamckis/Container-Security/assets/71128825/3647ab8b-acc4-4307-a048-6895c8d95c42)

### Privileged Flag
- This flag granbts all caabilities and removes isolation mechanisms.
- It is same as root privilege.
``` docker run --privileged -it <image-name> ```
- To run privileged contaainer in Kubernetes: </br>
![image](https://github.com/Vamckis/Container-Security/assets/71128825/2ea0a1c5-82c2-41f3-9542-c65b39d2b5af)

### SYS_ADMIN Capability
- SYS_ADMIN is a overloaded capability, referred as "new root"
- It has capabilities like mount, unmount, sethostname, setdomainname, swapon, pivot_root

## Capabilities Discovery:
- Once we are inside container, we can discover cpabilities allowed.
- Capabilkities can be viewed by reading content of mail container process PID=1, from within the cointainer:</br>
![image](https://github.com/Vamckis/Container-Security/assets/71128825/63ea1b7c-0e92-4faf-a039-1852a543b719)

- Capabilities are marked as BitMask. Each bit represents a different set of capabilities.
- Tool to discover and debug capabilities is ``capsh``
- 
### Reference:
- https://www.cybereason.com/blog/container-escape-all-you-need-is-cap-capabilities
- All Capabilities list: https://man7.org/linux/man-pages/man7/capabilities.7.html
