# Writing Components

### Component Types

The first step in writing a custom component is to choose what type of component you need. The component types are broken down by basic function. Almost all components you write will be one of the first three \(which are document transformers\). When creating a new component, choose the most specific type that meets your needs.

| Type | Description |
| :--- | :--- |
| `DocumentModifyingTransformer` | A document transformer that can do anything to the document passed to it.  It can delete, modify, and add fields to the document.  This transformer type also allows you to choose to drop the document. |
| `FieldValueCreatingTransformer` | A document transformer that creates new fields in the document based on existing fields. |
| `FieldValueModifyingTransformer` | A document transformer that modifies existing fields in the document.  This transformer type also allows you to choose to drop the document. |
| `MultiOutputDocumentTransformer` | An advanced document transformer that allows you to modify an existing "parent" document and to generate new "child" documents based on it.  The new documents will then flow through the system independent of the "parent" document. |
| `QueryTransformer` | A transformer that can modify queries before they are processed by the search engine. |
| `ResponseTransformer` | A transformer that can modify the resposnse to queries after they are processed by the search engine but before the response is returned to the user. |
| `BaseRoutingComponent` | An advanced component that can change the workflow that will be used for a system message. |
| `MessageHandlingWorkflowStage` | An advanced catch-all component that operates on raw system messages, doing whatever it likes to them. |

### The Mix-In Interfaces

Once you have chosen a component type, you can also add a number of mix-in interfaces to the component. These allow you to indicate additional capabilities or requirements to the platform for your component.

#### Lifecycle

| Name | Description |
| :--- | :--- |
| `Startable` | Provides a hook for the component to do initialization after its properties have been set before it does any processing. |
| `Stoppable` | Provides a hook for the component to clean up resources before system shutdown. |
| `AfterAllLocalInstancesStarted` | Provides a hook for the component to do initialization after all instances of this component have been started \(`Startable.startComponent()` has been called\). |
| `AfterLocalNodeStartup` | Provides a hook for the component to do initialization after all components in the system have been started. |

#### Component Configuration

| Name | Description |
| :--- | :--- |
| `HasBackoffLocaleProperty` | Provides option to set a default/backoff locale for component |
| `HasCaseModeProperty` | Provides option to set a case mode property for component |
| `HasDropDocumentOnExceptionProperty` | Provides option to configure document dropping when an exception occurs for component |
| `HasFieldMappingProperty` | Provides option to set a field mappings property for component |
| `HasFieldsProperty` | Provides option to set a list of fields for component |
| `HasInputListProperty` | Provides option to set a list of input fields for component |
| `HasInputProperty` | Provides option to set an input field for component |
| `HasOverwriteProperty` | Provides option to configure overwriting of existing values in output fields for component |
| `HasQueryLanguageProperty` | Provides option to set a query language \(simple, advanced, xml\) for component |
| `HasSchemaNameProperty` | Provides option to set a schema to validate against for component |
| `HasTokenizerProperty` | Provides option to set a tokenizer the component should use |

#### Miscellaneous

| Name | Description |
| :--- | :--- |
| `ComponentNameAware` | Indicates that the component needs to know what its component name is |
| `ProvidesProcessingFeedback` | Provides an option to set a [`ProcessFeedbackHandler`](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/server/component/ingest/ProcessingFeedbackHandler.html) for a component |
| `QualifiedComponentNameAware` | Indicates that the component needs to know what its qualified component name is |
| `SchemaUtilAware` | Provides a [`SchemaUtil`](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/server/util/SchemaUtil.html) object for a component to use |
| `SystemEventPublisherAware` | Provides a [`SystemEventPublisher`](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/server/util/SystemEventPublisher.html) object for a component to use |

#### Annotations

| Name | Description |
| :--- | :--- |
| `MultiOutputDocumentTransformerMode` | Used for document transformers that create multiple output documents or messages for each input document |
| `SingleInstancePerCluster` | Indicate that `maxInstances` is equal to 1 for this component across the entire topology |
| `SingleInstancePerNamedComponent` | Indicate that `maxInstances` per node is equal to 1 for this component for _each_ configuration of the class |
| `SingleInstancePerNode` | Indicate that `maxInstances` is equal to 1 for this component for each node the class/service is running on |
| `ThreadSafe` | Indicates that the component is thread safe and does not require an object pool |

