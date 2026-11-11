# INET vs UNIX Sockets

A **socket** is a way for programs to communicate with each other.

## INET Socket

Used for communication through a **network**.

It uses:

```text
IP address + port
```

Example:

```text
127.0.0.1:8080
```

- `127.0.0.1` → IP address
- `8080` → port

INET sockets can be used to communicate between different computers.

---

## UNIX Socket

Used for communication between programs on the **same computer**.

Instead of an IP address and port, it uses a **file path**.

Example:

```text
/run/app.sock
```

---

## Main Difference

```text
INET
→ IP address + port
→ Network communication

UNIX
→ File path
→ Same-computer communication
```

### Easy way to remember

**INET = network**

**UNIX = same machine**