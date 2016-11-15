# mx_vmar_unmap

## NAME

vmar_unmap - unmap a memory mapping

## SYNOPSIS

```
#include <magenta/syscalls.h>

mx_status_t mx_vmar_unmap(mx_handle_t vmar_handle,
                          uintptr_t addr, mx_size_t len);
```

## DESCRIPTION

**vmar_unmap**() unmaps all VMO mappings and destroys (as if **vmar_destroy**
were called) all sub-regions within the given range.  Note that this operation
is logically recursive.

## RETURN VALUE

**vmar_unmap**() returns **NO_ERROR** on success.

## ERRORS

**ERR_INVALID_ARGS**  *addr* or *len* are not page-aligned or *len* is 0.

**ERR_NOT_FOUND**  could not find the requested mapping

## NOTES

Currently *len* must be either 0, or *addr* and *len* must completely
describe either a single mapping or sub-region.  If *len* is 0, the unmap
is applied to the entire mapping that contains *addr*.

## SEE ALSO

[vmar_destroy](vmar_destroy.md).
[vmar_map](vmar_map.md).
[vmar_protect](vmar_protect.md).
