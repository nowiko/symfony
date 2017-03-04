UPGRADE FROM 3.2 to 3.3
=======================

ClassLoader
-----------

 * The component is deprecated and will be removed in 4.0. Use Composer instead.

Console
-------

* `Input::getOption()` no longer returns the default value for options
  with value optional explicitly passed empty.

  For:

  ```php
  protected function configure()
  {
      $this
          // ...
          ->setName('command')
          ->addOption('foo', null, InputOption::VALUE_OPTIONAL, '', 'default')
       ;
  }

  protected function execute(InputInterface $input, OutputInterface $output)
  {
      var_dump($input->getOption('foo'));
  }
  ```

  Before:

  ```
  $ php console.php command
  "default"

  $ php console.php command --foo
  "default"

  $ php console.php command --foo ""
  "default"

  $ php console.php command --foo=
  "default"
  ```

  After:

  ```
  $ php console.php command
  "default"

  $ php console.php command --foo
  NULL

  $ php console.php command --foo ""
  ""

  $ php console.php command --foo=
  ""
  ```

Debug
-----

 * The `ContextErrorException` class is deprecated. `\ErrorException` will be used instead in 4.0.

DependencyInjection
-------------------

 * Autowiring-types have been deprecated, use aliases instead.

   Before:

   ```xml
   <service id="annotations.reader" class="Doctrine\Common\Annotations\AnnotationReader" public="false">
       <autowiring-type>Doctrine\Common\Annotations\Reader</autowiring-type>
   </service>
   ```

   After:

   ```xml
   <service id="annotations.reader" class="Doctrine\Common\Annotations\AnnotationReader" public="false" />
   <service id="Doctrine\Common\Annotations\Reader" alias="annotations.reader" public="false" />
   ```

 * The `Reference` and `Alias` classes do not make service identifiers lowercase anymore.

 * Case insensitivity of service identifiers is deprecated and will be removed in 4.0.

 * Using the `PhpDumper` with an uncompiled `ContainerBuilder` is deprecated and
   will not be supported anymore in 4.0.

 * Extending the containers generated by `PhpDumper` is deprecated and won't be
   supported in 4.0.

 * The `DefinitionDecorator` class is deprecated and will be removed in 4.0, use
   the `ChildDefinition` class instead.

 * The ``strict`` attribute in service arguments has been deprecated and will be removed in 4.0.
   The attribute is ignored since 3.0, so you can simply remove it.

EventDispatcher
---------------

 * The `ContainerAwareEventDispatcher` class has been deprecated.
   Use `EventDispatcher` with closure-proxy injection instead.

Finder
------

 * The `ExceptionInterface` has been deprecated and will be removed in 4.0.

FrameworkBundle
---------------

 * The `Symfony\Bundle\FrameworkBundle\DependencyInjection\Compiler\AddConsoleCommandPass` has been deprecated. Use `Symfony\Component\Console\DependencyInjection\AddConsoleCommandPass` instead.

 * The `Symfony\Bundle\FrameworkBundle\DependencyInjection\Compiler\SerializerPass` class has been
   deprecated and will be removed in 4.0.
   Use the `Symfony\Component\Serializer\DependencyInjection\SerializerPass` class instead.

 * The `Symfony\Bundle\FrameworkBundle\DependencyInjection\Compiler\FormPass` class has been
   deprecated and will be removed in 4.0. Use the `Symfony\Component\Form\DependencyInjection\FormPass`
   class instead.

 * The `Symfony\Bundle\FrameworkBundle\EventListener\SessionListener` class has been
   deprecated and will be removed in 4.0. Use the `Symfony\Component\HttpKernel\EventListener\SessionListener`
   class instead.

 * The `Symfony\Bundle\FrameworkBundle\EventListener\TestSessionListener` class has been
   deprecated and will be removed in 4.0. Use the `Symfony\Component\HttpKernel\EventListener\TestSessionListener`
   class instead.

 * The `Symfony\Bundle\FrameworkBundle\DependencyInjection\Compiler\ConfigCachePass` class has been
   deprecated and will be removed in 4.0. Use `Symfony\Component\Config\DependencyInjection\ConfigCachePass`
   class instead.

 * The `Symfony\Bundle\FrameworkBundle\DependencyInjection\Compiler\PropertyInfoPass` class has been
   deprecated and will be removed in 4.0. Use the `Symfony\Component\PropertyInfo\DependencyInjection\PropertyInfoPass`
   class instead.

 * The `ConstraintValidatorFactory::$validators` and `$container` properties
   have been deprecated and will be removed in 4.0.

 * Extending `ConstraintValidatorFactory` is deprecated and won't be supported in 4.0.

HttpKernel
-----------

 * The `Psr6CacheClearer::addPool()` method has been deprecated. Pass an array
   of pools indexed by name to the constructor instead.

 * The `LazyLoadingFragmentHandler::addRendererService()` method has been
   deprecated and will be removed in 4.0.

 * The `X-Status-Code` header method of setting a custom status code in the
   response when handling exceptions has been removed. There is now a new
   `GetResponseForExceptionEvent::allowCustomResponseCode()` method instead,
   which will tell the Kernel to use the response code set on the event's
   response object.

Process
-------

 * The `ProcessUtils::escapeArgument()` method has been deprecated, use a command line array or give env vars to the `Process::start/run()` method instead.

 * Not inheriting environment variables is deprecated.

 * Configuring `proc_open()` options is deprecated.

 * Configuring Windows and sigchild compatibility is deprecated - they will be always enabled in 4.0.

 * Extending `Process::run()`, `Process::mustRun()` and `Process::restart()` is
   deprecated and won't be supported in 4.0.

Security
--------

 * The `RoleInterface` has been deprecated. Extend the `Symfony\Component\Security\Core\Role\Role`
   class in your custom role implementations instead.

SecurityBundle
--------------

 * The `FirewallContext::getContext()` method has been deprecated and will be removed in 4.0.
   Use the `getListeners()` method instead.

 * The `FirewallMap::$map` and `$container` properties have been deprecated and will be removed in 4.0.

 * The `UserPasswordEncoderCommand` command expects to be registered as a service and its
   constructor arguments fully provided.
   Registering by convention the command or commands extending it is deprecated and will
   not be allowed anymore in 4.0.

 * `UserPasswordEncoderCommand::getContainer()` is deprecated, and this class won't
    extend `ContainerAwareCommand` nor implement `ContainerAwareInterface` anymore in 4.0.

 * [BC BREAK] Keys of the `users` node for `in_memory` user provider are no longer normalized.

Serializer
----------

 * Extending `ChainDecoder`, `ChainEncoder`, `ArrayDenormalizer` is deprecated
   and won't be supported in 4.0.

TwigBridge
----------

 * The `TwigRendererEngine::setEnvironment()` method has been deprecated and will be removed
   in 4.0. Pass the Twig Environment as second argument of the constructor instead.

TwigBundle
----------

* The `ContainerAwareRuntimeLoader` class has been deprecated and will be removed in 4.0.
  Use the Twig `Twig_ContainerRuntimeLoader` class instead.

Workflow
--------

 * Deprecated class name support in `WorkflowRegistry::add()` as second parameter.
   Wrap the class name in an instance of ClassInstanceSupportStrategy instead.

Yaml
----

 * Omitting the key of a mapping is deprecated and will throw a `ParseException` in Symfony 4.0.

 * The constructor arguments `$offset`, `$totalNumberOfLines` and
   `$skippedLineNumbers` of the `Parser` class are deprecated and will be
   removed in 4.0