Design patterns are common solutions to recurring problems in software design. They provide a template for solving problems in a way that is proven to work. Below are some of the most commonly used design patterns in C#, along with explanations and sample code snippets.

### Creational Patterns

1. **Singleton Pattern**: Ensures a class has only one instance and provides a global point of access to it.

    ```csharp
    public class Singleton
    {
        private static Singleton _instance;

        private Singleton() { }

        public static Singleton Instance
        {
            get
            {
                if (_instance == null)
                {
                    _instance = new Singleton();
                }
                return _instance;
            }
        }
    }
    ```

2. **Factory Method Pattern**: Defines an interface for creating an object, but lets subclasses alter the type of objects that will be created.

    ```csharp
    public abstract class Product { }

    public class ConcreteProductA : Product { }
    public class ConcreteProductB : Product { }

    public abstract class Creator
    {
        public abstract Product FactoryMethod();
    }

    public class ConcreteCreatorA : Creator
    {
        public override Product FactoryMethod()
        {
            return new ConcreteProductA();
        }
    }

    public class ConcreteCreatorB : Creator
    {
        public override Product FactoryMethod()
        {
            return new ConcreteProductB();
        }
    }
    ```

3. **Abstract Factory Pattern**: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

    ```csharp
    public interface IAbstractFactory
    {
        IAbstractProductA CreateProductA();
        IAbstractProductB CreateProductB();
    }

    public class ConcreteFactory1 : IAbstractFactory
    {
        public IAbstractProductA CreateProductA()
        {
            return new ConcreteProductA1();
        }

        public IAbstractProductB CreateProductB()
        {
            return new ConcreteProductB1();
        }
    }

    public interface IAbstractProductA { }
    public interface IAbstractProductB { }

    public class ConcreteProductA1 : IAbstractProductA { }
    public class ConcreteProductB1 : IAbstractProductB { }
    ```

### Structural Patterns

1. **Adapter Pattern**: Allows incompatible interfaces to work together.

    ```csharp
    public interface ITarget
    {
        void Request();
    }

    public class Adaptee
    {
        public void SpecificRequest()
        {
            Console.WriteLine("Called SpecificRequest()");
        }
    }

    public class Adapter : ITarget
    {
        private readonly Adaptee _adaptee;

        public Adapter(Adaptee adaptee)
        {
            _adaptee = adaptee;
        }

        public void Request()
        {
            _adaptee.SpecificRequest();
        }
    }
    ```

2. **Decorator Pattern**: Adds behavior to objects dynamically.

    ```csharp
    public abstract class Component
    {
        public abstract void Operation();
    }

    public class ConcreteComponent : Component
    {
        public override void Operation()
        {
            Console.WriteLine("ConcreteComponent.Operation()");
        }
    }

    public abstract class Decorator : Component
    {
        protected Component _component;

        public Decorator(Component component)
        {
            _component = component;
        }

        public override void Operation()
        {
            _component.Operation();
        }
    }

    public class ConcreteDecoratorA : Decorator
    {
        public ConcreteDecoratorA(Component component) : base(component) { }

        public override void Operation()
        {
            base.Operation();
            Console.WriteLine("ConcreteDecoratorA.Operation()");
        }
    }
    ```

3. **Facade Pattern**: Provides a simplified interface to a complex subsystem.

    ```csharp
    public class SubsystemA
    {
        public void OperationA()
        {
            Console.WriteLine("SubsystemA Operation");
        }
    }

    public class SubsystemB
    {
        public void OperationB()
        {
            Console.WriteLine("SubsystemB Operation");
        }
    }

    public class Facade
    {
        private readonly SubsystemA _subsystemA;
        private readonly SubsystemB _subsystemB;

        public Facade()
        {
            _subsystemA = new SubsystemA();
            _subsystemB = new SubsystemB();
        }

        public void Operation()
        {
            _subsystemA.OperationA();
            _subsystemB.OperationB();
        }
    }
    ```

### Behavioral Patterns

1. **Strategy Pattern**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable.

    ```csharp
    public interface IStrategy
    {
        void Execute();
    }

    public class ConcreteStrategyA : IStrategy
    {
        public void Execute()
        {
            Console.WriteLine("Strategy A");
        }
    }

    public class ConcreteStrategyB : IStrategy
    {
        public void Execute()
        {
            Console.WriteLine("Strategy B");
        }
    }

    public class Context
    {
        private IStrategy _strategy;

        public Context(IStrategy strategy)
        {
            _strategy = strategy;
        }

        public void SetStrategy(IStrategy strategy)
        {
            _strategy = strategy;
        }

        public void ExecuteStrategy()
        {
            _strategy.Execute();
        }
    }
    ```

2. **Observer Pattern**: Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

    ```csharp
    public interface IObserver
    {
        void Update();
    }

    public class ConcreteObserver : IObserver
    {
        public void Update()
        {
            Console.WriteLine("Observer Updated");
        }
    }

    public interface ISubject
    {
        void Attach(IObserver observer);
        void Detach(IObserver observer);
        void Notify();
    }

    public class ConcreteSubject : ISubject
    {
        private List<IObserver> _observers = new List<IObserver>();

        public void Attach(IObserver observer)
        {
            _observers.Add(observer);
        }

        public void Detach(IObserver observer)
        {
            _observers.Remove(observer);
        }

        public void Notify()
        {
            foreach (var observer in _observers)
            {
                observer.Update();
            }
        }
    }
    ```

3. **Command Pattern**: Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.

    ```csharp
    public interface ICommand
    {
        void Execute();
    }

    public class ConcreteCommand : ICommand
    {
        private readonly Receiver _receiver;

        public ConcreteCommand(Receiver receiver)
        {
            _receiver = receiver;
        }

        public void Execute()
        {
            _receiver.Action();
        }
    }

    public class Receiver
    {
        public void Action()
        {
            Console.WriteLine("Receiver Action");
        }
    }

    public class Invoker
    {
        private ICommand _command;

        public void SetCommand(ICommand command)
        {
            _command = command;
        }

        public void ExecuteCommand()
        {
            _command.Execute();
        }
    }
    ```

These are just a few of the common design patterns used in C#. Each pattern provides a template for solving a particular design problem, and they can be adapted to fit specific needs. Design patterns are useful for creating flexible and reusable code.
