[Home](../README.md)

# Django Rest Framework Guidance

## 资源和文档

[DRF Homepage & Document](https://www.django-rest-framework.org/)

## 功能

我们将主要使用 Django Rest Framework 的以下功能

- [ViewSets](https://www.django-rest-framework.org/api-guide/viewsets/)  
  Django REST framework allows you to combine the logic for a set of related views in a single class, called a ViewSet.
- [Serializers](https://www.django-rest-framework.org/api-guide/serializers/)  
  Serializers allow complex data such as querysets and model instances to be converted to native Python datatypes that can then be easily rendered into JSON, XML or other content types. Serializers also provide deserialization, allowing parsed data to be converted back into complex types, after first validating the incoming data.
- [Permissions](https://www.django-rest-framework.org/api-guide/permissions/)  
  Together with authentication and throttling, permissions determine whether a request should be granted or denied access.
- [Pagination](https://www.django-rest-framework.org/api-guide/pagination/)  
  REST framework includes support for customizable pagination styles. This allows you to modify how large result sets are split into individual pages of data.
- [Filtering](https://www.django-rest-framework.org/api-guide/filtering/)  
  The default behavior of REST framework's generic list views is to return the entire queryset for a model manager. Often you will want your API to restrict the items that are returned by the queryset.
