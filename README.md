## What 
Example `.yaml` files from Kubernetes Up and Running, 2nd Ed, but adapted to work with Kubernets v1.17

Adapted for issues such as:

`error: unable to recognize "kuard-rs.yaml": no matches for kind "ReplicaSet" in version "extensions/v1beta1"`

* `extensions/v1beta1` is no longer valid for apiVersion as of Kubernetes 1.16
  * https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/#writing-a-replicaset-manifest

`error: error validating "kuard-rs.yaml": error validating data: ValidationError(ReplicaSet.spec): missing required field "selector" in io.k8s.api.apps.v1.ReplicaSetSpec`

* `ReplicaSet`s appear to need a `spec.selector` now
  * https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/#example

Used against:

```yaml
# kubectl version -o json

{
  "clientVersion": {
    "major": "1",
    "minor": "17",
    "gitVersion": "v1.17.3",
    "gitCommit": "06ad960bfd03b39c8310aaf92d1e7c12ce618213",
    "gitTreeState": "clean",
    "buildDate": "2020-02-11T18:14:22Z",
    "goVersion": "go1.13.6",
    "compiler": "gc",
    "platform": "linux/amd64"
  },
  "serverVersion": {
    "major": "1",
    "minor": "17",
    "gitVersion": "v1.17.2",
    "gitCommit": "59603c6e503c87169aea6106f57b9f242f64df89",
    "gitTreeState": "clean",
    "buildDate": "2020-01-18T23:22:30Z",
    "goVersion": "go1.13.5",
    "compiler": "gc",
    "platform": "linux/amd64"
  }
}
```

Errata:  
https://www.oreilly.com/catalog/errataunconfirmed.csp?isbn=0636920223788  

---

#### Pg. 161-162 Regex issue
The example Regex given isn't even valid, it's like someone forgot to close opening `[` with `]` and it slipped past editors?..:

`^[.[?[a-azAz0-9[([.[?[a-zA-Z0-9[+[-_a-zA-Z0-9[?)*$`

But even when you fix the `[`s that should be `]`s it still doesn't match the example valid key names on p. 162:
 
`^[.]?[a-zAZ0-9]([.]?[a-zA-Z0-9]+[-_a-zA-Z0-9]?)*$`

Here is a seemingly better working Regex:  

`^[^_]\.?(\w+|\d+)[-._](\w+|\d+)?$`

https://regex101.com/r/108DPe/4 
