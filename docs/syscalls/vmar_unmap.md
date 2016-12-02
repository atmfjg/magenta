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
is logically recursive.  It is an error to call this with a range that partially
overlaps a sub-region.  If this call partially overlaps a VMO mapping, only
the overlapped portion will be unmapped.

## RETURN VALUE

**vmar_unmap**() returns **NO_ERROR** on success.

## ERRORS

**ERR_INVALID_ARGS**  *addr* or *len* are not page-aligned, *len* is 0, or the
range partially overlaps a sub-region.

**ERR_BAD_STATE**  *vmar_handle* refers to a destroyed handle

**ERR_NOT_FOUND**  could not find the requested mapping

## NOTES

## SEE ALSO

[vmar_destroy](vmar_destroy.md).
[vmar_map](vmar_map.md).
[vmar_protect](vmar_protect.md).
