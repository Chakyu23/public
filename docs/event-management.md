# Events management

## Usage

An event is associated to an object when the usage of this object implies:

- a limited capacity of people
- a limited time

Event management require:

- Edition of the attributes of the object on which the event is based
- Creation and settings of the event associated to the reference object

> Events are used for: `piscines`, `check-in`, `exams`, `rushes`, `hackatons`, `conferences`.

## Settings for the reference object

Important indications:

- Objects that doesn't have required attributes for event creation will not be open to event creation.

| name                 | fullfillment |
| -------------------- | ------------ |
| capacity             | **required** |
| eventDuration        | **required** |
| registrationDuration | **required** |
| description          | optionnal    |
| eventStartDelay      | optionnal    |

- All the attributes filled in the object are used as values by default for event's creation; it can be overloaded for each event related to the reference object.
- If the reference object has a child or children which are events itself, settings are also required for each event child.

#### Edit the object attributes:

> in _Object attributes_

<img width="1073" alt="Capture d’écran 2019-08-22 à 11 40 34" src="img/63525316-64e0da80-c4f5-11e9-9e61-57d5a73da9b1.png">

- Add a new key **capacity** of type `Number` with the maximum number of persons you want for events related to the object by default
- Add a new key **eventDuration** of type `Number` with the duration in minutes you want for events related to the object by default
- Add a new key **registrationDuration** of type `Number` with the duration in minutes you want to allow to people to register to the event by default
- Add a new key **eventStartDelay** of type `Number`, if you want a default delay between the end of registration and the beginning of the event. This duration is expressed in minutes.
- Add a new key **description** of type `String`, if you need to associate some informations to your event (description, location, access, documents to provide, etc.)

#### Edit the children

> in _Children_

<img width="609" alt="Capture d’écran 2019-08-22 à 15 43 43" src="img/63525543-c86b0800-c4f5-11e9-8820-60d9ff33994f.png">

- Add a new key **startAfter** of type `Number`, with the default delay you want between the beginning of the event and the beginning of the child event. This duration is expressed in minutes.

##### Example

Here is an example of the `Piscine Go` settings. It presents the settings of the object attributes `Piscine Go`, the settings of one of its child which is an event and the settings of the child object attributes itself.

> NB : this object settings are provided in the admin, in the curses section: 'Piscine Go' and in the exams section 'Exam 01'.

**Piscine Go**

_Object attributes_

```json
{
  "capacity": 400,
  "eventDuration": 37440,
  "registrationDuration": 43200,
  "eventStartDelay": 240
}
```

This piscine object attributes look like this:

![piscine-object-attributes](img/piscine-object-attributes.png)

_Children_

> In the `Piscine Go`, children of type _exam_ and _rush_ have events itself.

> A **startAfter** key has to be defined for each of them, in their parent object `Piscine Go`. For example, the exam-01 gets this key:

```json
{
  "startAfter": 8160
}
```

This child attributes look like this:

![piscine children attributes](img/63525543-c86b0800-c4f5-11e9-8820-60d9ff33994f.png)

**Exam 01**

> The object `Exam 01`, which is a child of `Piscine Go`, has its own _Object Attributes_ filled in the child object.

_Object attributes_

```json
{
  "eventDuration": 240,
  "registrationDuration": 2160,
  "eventStartDelay": 60
}
```

> NB: the **capacity** attribute is herited from the parent object `Piscine Go` here.

This exam object attributes look like this:

![exam-object-attributes](img/exam-object-attributes.png)

## Create the event

### Create a new event for your object

> (in _Admin_ > _Manage events_ > _Add new event_)

<img width="788" alt="Capture d’écran 2019-08-22 à 11 37 13" src="img/63532891-9d87b080-c503-11e9-8ff2-46c7a5b19c12.png">
<img width="789" alt="Capture d’écran 2019-08-22 à 11 37 35" src="img/63533088-02430b00-c504-11e9-9675-bcab7bec825c.png">
<img width="787" alt="Capture d’écran 2019-08-22 à 11 38 07" src="img/63533145-21419d00-c504-11e9-8e80-fb4f53d93b00.png">

- The **reference object** of your event is the object for which you need to create an event: `Check`, `Piscine Go`, etc.
- The **registration starts at** indicates when registration of the event begins.
- The **registration ends at** indicates when registration of the event ends.
- The **event starts at** indicates when the event begins.

> NB:
>
> - End of registration can't be before its beginning.
> - Start of event can't be before end of registration.
> - Date and Time input is not yet working in firefox but should be added soon by mozilla. In the mean while use chrome for adding events

### Settings for you event

> In the event you have created, 3 categories must be checked:
>
> 1. General settings
> 2. Registration's settings
> 3. Event's settings

#### General settings

<img width="785" alt="Capture d’écran 2019-08-22 à 11 39 26" src="img/63533589-015ea900-c505-11e9-8b77-b45b620cd171.png">

General settings of your event can be set after creation of the event. By default, it is the values indicated in the **reference object**.

- **Capacity**
  - During the regitration, the capacity doesn't apply. When registration ends, we register the amount defined by the **capacity** to the event _(ordered by registration date)_.
    - If someone unregister to the event during a registration, it release one place.
    - During a registration, users can see if their place is guaranteed or if they are in waiting list.
  - If the event has children which are event themselves, they will use by default the capacity of the parent event
    if no capacity was defined on this child.
- **Description** (facultative)
  - It can be used to describe the topic of the event, or to add some practical informations: location, documents to provide, accessibility, etc.

#### Registration

<img width="761" alt="Capture d’écran 2019-08-22 à 11 39 37" src="img/63533613-0facc500-c505-11e9-90e8-94254cef5ce3.png">

- End of registration can't be after start of registration.
- Dates can't be updated after it's passed.
- The **registration duration** indicated in the **reference object** is reminded under the inputs to help you fill the informations.
- Same for the **event start delay**.
- The list of users in the registration, pending or accepeted, is accessible by clicking on the link 'N users registered', at the left bottom of this categrory.

#### Event

<img width="740" alt="Capture d’écran 2019-08-22 à 11 39 49" src="img/63533641-1d624a80-c505-11e9-9cd1-e1d156dd7fc4.png">

- End of event can't be after start of event.
- Dates can't be updated after it's passed.
- The **end of event** is calculated by default by adding the **event duration** indicated in the **reference object** to the **start of event** date.
  - If the event contains other events, the **end of event** can't be before the end of the last child event.
- The **event duration** indicated in the **reference object** is reminded under the inputs to help you fill the informations.
  - If the event contains other events, the **minimum end of event** is indicated under the inputs to help you fill the informations.
- The list of users selected for the event at its creation is accessible by clicking on the link 'N users registered', at the left bottom of this categrory.

#### Children (facultative)

<img width="1009" alt="Capture d’écran 2019-08-22 à 18 24 49" src="img/63535788-29044000-c50a-11e9-835c-f8378558962c.png">

This category appears only if the event has children which are events itself.

- Children settings can't be overloaded.
- Each event child presents:
  - Its **Start** and **end** (according to the children settings of the **reference object**)
  - Its **capacity**
  - Its **groups size**
    - Reminder: in `hackatons` or `rushes`, candidates or students registered to the are divided in groups of N persons.
