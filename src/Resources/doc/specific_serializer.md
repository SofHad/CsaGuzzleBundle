Using specific serializer
=========================

By default Guzzle allow you to set a specific variable in the JSON configuration of a rezquest.
It will be automatically be transformed to JSON with the ```json_encode``` method of PHP.

If you want to send complex objects with different view or receive some data in the right format, you have to
use a serializer.

There is two well know serializer:
- the (serializer component)[http://symfony.com/doc/current/components/serializer.html] in Symfony
- the (JMS Serializer)[http://jmsyst.com/libs/serializer]

To use a serializer you have to use an adapter. By default an adapter is provided for the serializer component and
an other one for the JMS Serializer.

Configuration
-------------

You can set a serializer for all your clients:

```yml
csa_guzzle:
    serializer:
        adapter: csa_guzzle.serializer.adapter.jms
```

Or for a specific client:

```yml
csa_guzzle:
    clients:
        github_api:
            serializer:
                adapter: csa_guzzle.serializer.adapter.symfony
```

Usage
-----

```php
public function indexAction(Request $request)
{
    $client = $this->get('csa_guzzle.client.github_api');
    $data = $client->requestAsync(
        'GET',
        '/api/test',
        [
            'json' => ['foo' => 'bar'],
            'serialization' => ['type' => 'array']
        ]
    );
}
```

In this example, ```$data``` will contain an array






