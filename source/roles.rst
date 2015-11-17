.. _roles-label:

============
Roles
============

There are four built-in **Roles** contained in **Coach**. These are:

* System Administrator
* Application Administrator
* Manager
* Agent

.. danger::

  |  Currently **Roles** can only be assigned through [User](/v1/user), but only *administrative* **Roles** (*System Administrator*, *Application Administrator*).
  |  The **Roles** *Manager* and *Agent* are not assigned as **Role** but rather as :ref:`unit-label`/:ref:`team-label` *managership* for *Manager* and/or :ref:`team-label` *membership* for *Agent*.
  |  The [User](/v1/user) is *Manager* as long as he or she is assigned as manager of at least one or more :ref:`unit-label` or :ref:`team-label`.
  |  The [User](/v1/user) is *Agent* as long as he or she is assigned as member of at least one or more :ref:`team-label`.


Each Role has a different purpose with correspondingly different levels of access to **Coach** Console and **Coach** QM. These levels of access are called *Permissions*.
Multiple **Roles** can be assigned to the same User, the differing Permissions for differing **Role** being combined with one another

System Administrator
====================

During the **Coach** installation process a [User](/v1/user) with the **Role** of *System Administrator* is created. This *System Administrator* can only enter **Coach** *Console* for :ref:`tenant-label` 1000, the original host :ref:`tenant-label`. Here they have full permissions within **Coach** *Console* for every extant :ref:`tenant-label` and can add new :ref:`Tenants <tenant-label>` as well as view, edit and delete any that have been created.

Apart from the *System Administrator* created during **Coach**’s installation [User](/v1/user)s can only be added manually to the *System Administrator* **Role**. The **Role** can be assigned to any [User](/v1/user) but it can only be assigned by, and is only visible to, [User](/v1/user)s who already have the **Role**. Due to the importance of this **Role** for the **Coach** application, a *System Administrator* cannot un-assign themself from the **Role** of *System Administrator* (or any other **Role** they may have been given) – only a fellow *System Administrator* can perform this action, thereby ensuring that at least one [User](/v1/user) always has the *System Administrator* **Role** in each installation. For the same reason a *System Administrator* can only be deactivated by another *System Administrator*.

Application Administrator
=========================

When a new :ref:`tenant-label` is created an *Application Administrator* must be created. An *Application Administrator* can access both **Coach** Console and **Coach** *QM* for the :ref:`tenant-label` they were created for. In **Coach** Console they have full permissions excepting the ability to add new :ref:`Tenants <tenant-label>` or delete their own. In **Coach** *QM* they have full permissions except that they cannot create Evaluations or **Coaching Sessions**.

Apart from the *Application Administrator* created with a new :ref:`tenant-label` further [User](/v1/user)s can only be added manually to the *Application Administrator* **Role**. Due to the importance of this **Role** for a :ref:`tenant-label`, an *Application Administrator* cannot un-assign themselves from the **Role** of *Application Administrator* (or any other **Role** they may have been given) – only a fellow *Application Administrator* (or a *System Administrator*) can perform this action, thereby ensuring that at least one [User](/v1/user) always has the *Application Administrator* (or *System Administrator*) **Role** within each :ref:`tenant-label`. For the same reason an *Application Administrator* can only be deactivated by another *Application Administrator* (or a *System Administrator*).

Manager
=======

A *Manager* can only enter **Coach** *QM*. Here they can view everything but can only create, edit and delete *Evaluations*, *Coaching Sessions* and *Reports* for the [User](/v1/user)s they manage. [User](/v1/user)s are automatically assigned to the *Manager* **Role** when they are made *Manager* of a :ref:`team-label` or Unit.

Agent
=====

An *Agent* can only enter **Coach** *QM* and can only access *Evaluations* and *Coaching Sessions* created for them. [User](/v1/user)s are automatically assigned to the *Agent* **Role** when they are joined to a :ref:`team-label`.
