# mx_vmar_protect

## NAME

vmar_protect - set protection of a memory mapping

## SYNOPSIS

```
#include <magenta/syscalls.h>

mx_status_t mx_vmar_protect(mx_handle_t vmar_handle,
                            uintptr_t addr, mx_size_t len,
                            uint32_t prot);
```

## DESCRIPTION

**vmar_protect**() alters the access protections for the memory mapping
at *addr*. The *prot* argument should be a bitwise-or of one or more of
the following:
- **MX_VM_FLAG_PERM_READ**  Map as readable.  It is an error if *vmar*
  does not have *MX_VM_FLAG_CAN_MAP_READ* permissions or the *vmar* handle does
  not have the *MX_RIGHT_READ* right.
- **MX_VM_FLAG_PERM_WRITE**  Map as writable.  It is an error if *vmar*
  does not have *MX_VM_FLAG_CAN_MAP_WRITE* permissions or the *vmar* handle does
  not have the *MX_RIGHT_WRITE* right.
- **MX_VM_FLAG_PERM_EXECUTE**  Map as executable.  It is an error if *vmar*
  does not have *MX_VM_FLAG_CAN_MAP_EXECUTE* permissions or the *vmar* handle does
  not have the *MX_RIGHT_EXECUTE* right.

Behavior is undefined if *addr* was not mapped via the **vmar_map**()
function.

## RETURN VALUE

**vmar_protect**() returns **NO_ERROR** on success.

## ERRORS

**ERR_INVALID_ARGS**  *prot* is an unsupported combination of flags
(e.g., PROT_WRITE but not PROT_READ), *addr* or *len* are not page-aligned,
or *len* is 0.

**ERR_NOT_FOUND**  could not find the requested mapping

**ERR_ACCESS_DENIED**  *vmar_handle* does not have **MX_RIGHT_WRITE**.

## NOTES

Currently the *len* parameter is ignored, and the entire region that was
mapped is altered.

## SEE ALSO

[vmar_map](vmar_map.md).
[vmar_unmap](vmar_unmap.md).
