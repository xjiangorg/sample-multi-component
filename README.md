### Sample multi component git repository.

To test multi component build from the same git repository create the following objects:

#### Application

```yaml
apiVersion: appstudio.redhat.com/v1alpha1
kind: Application
metadata:
  name: application-sample
  namespace: test
spec:
  description: Simple app that consists from two components from the same git repository
  displayName: test-git-multi-component
```

#### Component 1

```yaml
apiVersion: appstudio.redhat.com/v1alpha1
kind: Component
metadata:
  name: go-component-sample
  namespace: test
  annotations:
    build.appstudio.openshift.io/request: "configure-pac"
    image.redhat.com/generate: '{"visibility": "public"}'
spec:
  componentName: go-sample-component-name
  application: application-sample
  source:
    git:
      url: https://github.com/mmorhun/sample-multi-component
      context: go-component
```

#### Component 2

```yaml
apiVersion: appstudio.redhat.com/v1alpha1
kind: Component
metadata:
  name: python-component-sample
  namespace: test
  annotations:
    build.appstudio.openshift.io/request: "configure-pac"
    image.redhat.com/generate: '{"visibility": "public"}'
spec:
  componentName: python-sample-component-name
  application: application-sample
  source:
    git:
      url: https://github.com/mmorhun/sample-multi-component
      context: python-component
```

