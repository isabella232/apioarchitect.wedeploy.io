---
title: "Providers"
order: 3
---

A Provider is an extension point in Apio Architect that lets you extract and reuse values from the request, rather than extracting such values each time you need them. Apio Architect providers follow the same approach as JAX-RS context providers. 

To create an Apio Architect provider, implement the `Provider` interface and register the class as a `Provider` service component in OSGi. This interface has a parameter for the type of value to extract from the request, and a single method (`createContext`) for extracting that value. 

This example Provider extracts an `ApplicationURL` from the request: 

```java
@Component(service = Provider.class)
public class ApplicationURLProvider implements Provider<ApplicationURL> {

	@Override
	public ApplicationURL createContext(HttpServletRequest httpServletRequest) {
		return getServerURL(httpServletRequest) + httpServletRequest.getContextPath();
	}

}
```

After deploying this component, Apio Architect can inject the `ApplicationURL` in all the [actions](/docs/reference/actions.html) that need it. 
