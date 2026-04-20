# Session Notes

## Scaling

- **Vertical scaling**: Increasing the resources of the same instance, such as changing from `t3.micro` to `t3.large`.
- Vertical scaling usually involves downtime, and there is always a limit to how much a single server can be upgraded.
- **Horizontal scaling**: Adding more similar resources so workloads can be distributed across multiple servers.
- Horizontal scaling is designed to reduce or avoid downtime and is generally more flexible.

- If the created server is a **Spot Instance**, you cannot scale it vertically because you cannot change the instance type.

## Keeping the Public IP Address Same

- To keep the public IP address of an EC2 instance the same all the time, use an **Elastic IP Address**.
- An Elastic IP reserves a static public IP that can be assigned to the server.
- This keeps the public IP unchanged even if the instance is stopped and started.
- Keep in mind that Elastic IP addresses are not free, and you may be billed for them even when the server is off.
- Because of the cost, many people avoid using Elastic IPs unless they really need a fixed public IP.

## Non-Functional Requirement

Going forward, we will be using:

- Launch Template with `B60-LabImage-RHEL9` using **Spot**.
- Security group: `b60-allow-all`.
- New instances will be launched regularly for sessions and for the project.

## Points to Note Before Learning Linux

- Linux is case-sensitive, for example: `ec2-user` and `Ec2-user` are different.
- In Linux, everything is a file: commands, binaries, and files.
- In Linux, every configuration is stored in a file.
- If something does not work as expected, think about the reason and fix it by updating the relevant file or configuration.
- In Linux, almost all operations are done using command line commands.
- Start, stop, and restart are all done using commands.
- File creation, update, and deletion are done using commands.
- Folder creation, update, and deletion are done using commands.
- Each command is created by different people, which is why every command has its own manual.

## Learning Approach

- Watch the session one more time.
- Then practice the commands and concepts yourself.