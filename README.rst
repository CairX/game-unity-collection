#######################
Game - Unity Collection
#######################
This repository is my personal notebook containing scribbles about the Unity game engine.
During the short time I have been using the engine it feels like I have spent equal parts doing developing as I have been doing research.
There is some useful information that I would like to remember, because I will without a doubt forget some if it, so here are my notes.

.. contents:: Table of Contents
.. section-numbering::


*****************
Extension Methods
*****************
Feature of the C# language, I recommend reading `this guide <https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/extension-methods>`_ over at Microsoft Docs for further details.
Following examples will show have it can be used to extend functionality to predefined components in Unity.


Example - Vector3
=================
In order to change one value of a ``Vector3`` you have to create a new ``Vector3`` object.
An example would that you want to change just the ``z`` value of the ``transform.position``.
Originally you would write something like the following.

.. code:: csharp

    transform.position = new Vector3(transform.position.x, transform.position.y, 0);

With extension methods it's possible to make it a little less verbose.
To me it also becomes less error prone, know that I have copy and pasted the above a few times and every now and again a value isn't correctly modified.

.. code:: csharp

    transform.position = transform.position.ChangeZ(0);

Not all that much difference but do it several times and it's kinda convenient.
The following shows how to set it up.

.. code:: csharp

    using UnityEngine;

    public static class VectorExtensions {
        public static Vector3 ChangeX(this Vector3 vector, float x) {
            return new Vector3(x, vector.y, vector.z);
        }

        public static Vector3 ChangeY(this Vector3 vector, float y) {
            return new Vector3(vector.x, y, vector.z);
        }

        public static Vector3 ChangeZ(this Vector3 vector, float z) {
            return new Vector3(vector.x, vector.y, z);
        }
    }

Example - Transform
===================
Extension methods also allow for direct modification in contrast to the example of extending ``Vector3``.

.. code:: csharp
    
    transform.Reset();

The following shows how to set it up.

.. code:: csharp

    using UnityEngine;

    public static class TransformExtensions {
        public static void Reset(this Transform transform) {
            transform.position = Vector3.zero;
            transform.localRotation = Quaternion.identity;
            transform.localScale = new Vector3(1, 1, 1);
        }
    }
