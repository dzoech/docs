---
acl_categories:
- '@read'
- '@stream'
- '@slow'
arguments:
- display_text: key
  key_spec_index: 0
  name: key
  type: key
- display_text: group
  name: group
  type: string
arity: 4
command_flags:
- readonly
complexity: O(1)
description: Returns a list of the consumers in a consumer group.
group: stream
hidden: false
hints:
- nondeterministic_output
history:
- - 7.2.0
  - Added the `inactive` field.
key_specs:
- RO: true
  access: true
  begin_search:
    spec:
      index: 2
    type: index
  find_keys:
    spec:
      keystep: 1
      lastkey: 0
      limit: 0
    type: range
linkTitle: XINFO CONSUMERS
since: 5.0.0
summary: Returns a list of the consumers in a consumer group.
syntax_fmt: XINFO CONSUMERS key group
syntax_str: group
title: XINFO CONSUMERS
---
This command returns the list of consumers that belong to the `<groupname>` consumer group of the stream stored at `<key>`.

The following information is provided for each consumer in the group:

* **name**: the consumer's name
* **pending**: the number of entries in the PEL: pending messages for the consumer, which are messages that were delivered but are yet to be acknowledged
* **idle**: the number of milliseconds that have passed since the consumer's last attempted interaction (Examples: [`XREADGROUP`](/commands/xreadgroup), [`XCLAIM`](/commands/xclaim), [`XAUTOCLAIM`](/commands/xautoclaim))
* **inactive**: the number of milliseconds that have passed since the consumer's last successful interaction (Examples: [`XREADGROUP`](/commands/xreadgroup) that actually read some entries into the PEL, [`XCLAIM`](/commands/xclaim)/[`XAUTOCLAIM`](/commands/xautoclaim) that actually claimed some entries)

## Examples

```
> XINFO CONSUMERS mystream mygroup
1) 1) name
   2) "Alice"
   3) pending
   4) (integer) 1
   5) idle
   6) (integer) 9104628
   7) inactive
   8) (integer) 18104698
2) 1) name
   2) "Bob"
   3) pending
   4) (integer) 1
   5) idle
   6) (integer) 83841983
   7) inactive
   8) (integer) 993841998
```