# Capabilities
- Capabilities provide ability to give a small set of privileges to a thread/ process.
- All privileged actions are categorised into 40 capabilities.
- Purpose of capabilities is to divide root privileges into dustinct privileges.

Below is the image showing privileges breakdown in container:
![Privileges_Breakdown](https://github.com/Vamckis/Container-Security/assets/71128825/88e85dc3-a8f8-4b2e-af35-5f7e387500fe)

### Capabilities Commands
- With Docker Runtime:
``` docker run --cap-add=<CAP> -it <Image name> ```
``` docker run --cap-add ALL -it <Image name> ```
``` docker run --cap-drop=<CAP> -it <Image name> ```
``` docker run --cap-add ALL -it <Image name> ```
- With Kubernetes, we can add/drop in Security Context
![image](https://github.com/Vamckis/Container-Security/assets/71128825/3647ab8b-acc4-4307-a048-6895c8d95c42)

### SYS_ADMIN
- SYS_ADMIN is a overloaded capability, referred as "new root"
- It has capabilities like mount, unmount, sethostname, setdomainname, swapon, pivot_root

  
### Reference:
- https://www.cybereason.com/blog/container-escape-all-you-need-is-cap-capabilities
- All Capabilities list: https://man7.org/linux/man-pages/man7/capabilities.7.html
