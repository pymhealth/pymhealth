.. highlight:: python3
========
Location
========

--------
Distance
--------
Distance formula between latitude and longitude points given in decimal degrees. Additionally, vectorised JIT compiled functions are provided: 

* elementwise: elementwise distance between latitude and longitude vectors
* vector: distance between a single fixed location and vectors for compared latitudes and longitudes
* outer_product: The distance outer product between two sets of latitude/longitude vectors

Metrics:

* `Haversine`_
* Karney TODO


Haversine
---------
Haversine gives the great-circle distance between two points on a sphere.

:math:`d = 2r \cdot \arcsin (\sqrt{\sin^2(\frac{\phi_2 - \phi_1}{2}) + \cos(\phi_1) \cdot \cos(\phi_2) \cdot \sin^2(\frac{\lambda_2 - \lambda_1}{2})})`

The radius of the earth varies, so the mean radius is used (6371.009 km - same as geopy). The calculated distance should be accurate within ~0.5%


.. py:function:: haversine(lat1, lon1, lat2, lon2)
    Find the haversine distance in kilometers between the points
    (lat1, lon1) and (lat2, lon2) given in degrees.

    :param lat1: latitude of first point
    :type lat1: float
    :param lon1: longitude of first point
    :type lon1: float
    :param lat2: latitude of second point
    :type lat2: float
    :param lon2: longitude of second point
    :type lon2: float
    :rtype: float64

Example:
::
    >>> from mhealth.processing.location.distance import haversine
    >>> haversine(41.507483, -99.436554, 38.504048, -98.315949)
    347.32834803942626
    >>> london = (51.5074, 0.1278)
    >>> paris = (48.8566, 2.3522)
    >>> haversine(*london, *paris)
    334.57613798049994

------------

.. py:function:: haversine_elementwise(lat1, lon1, lat2, lon2)
    The haversine elementwise distance between two sets of
    latitude and longitude vectors.

    :param lat1: vector of latitudes
    :type lat1: float64[n]
    :param lon1: vector of longitudes
    :type lon1: float64[n]
    :param lat2: vector of latitudes
    :type lat2: float64[n]
    :param lon2: vector of longitudes
    :type lon2: float64[n]
    :rtype: float64[n]

For example, to find the distance between successive points:
::
    >>> from mhealth.processing.location.distance import haversine_elementwise
    >>> lats = [0.123, -43.23, 88.09, 51.23] # (It is preferable to provide numpy arrays.)
    >>> lons = [160.1, 99.12, 1.12, -20.1]
    >>> haversine_elementwise(lats[1:], lons[1:], lats[:-1], lons[:-1])
    array([ 7715.92891568, 14840.77608768,  4113.65086425])

------------

.. py:function:: haversine_vector(lat1, lon1, latcol, loncol)
    The haversine distance between a fixed point and a set of
    latitude / longitude vectors

    :param lat1: fixed latitude
    :type lat1: float64
    :param lon1: fixed longitude
    :type lon1: float64
    :param latcol: latitude vector
    :type latcol: float64[n]
    :param loncol: longitude vector
    :type loncol: float64[n]
    :rtype: float64[n]

Example:
::
    >>> from mhealth.processing.location.distance import haversine_vector
    >>> lats = [0.123, -43.23, 88.09, 51.23] # (It is preferable to provide numpy arrays.)
    >>> lons = [160.1, 99.12, 1.12, -20.1]
    >>> haversine_vector(lats[0], lons[0], lats[1:], lons[1:])
    array([ 7715.92891568, 10192.11206194, 14304.8626077 ])

------------

.. py:function:: haversine_outer_product(lat1, lon1, lat2, lon2)
    The haversine distance between every element of two sets of
    latitude/longitude vectors

    :param lat1: latitude vector
    :type lat1: float64[n]
    :param lon1: longitude vector
    :type lon1: float64[n]
    :param lat2: latitude vector
    :type lat2: float64[m]
    :param lon2: longitude vector
    :type lon2: float64[m]
    :rtype: float64[n,m]

For example, to find the pairwise distance of a list of points:
::
    >>> import numpy as np
    >>> from mhealth.processing.location.distance import haversine_outer_product
    >>> points = np.array([[0.123, 21.432], [54.54, 65.6], [-5.0, -10.0]])
    >>> haversine_outer_product(points[:, 0], points[:, 1], points[:, 0], points[:, 1])
    array([[   0.        , 7260.9522096 , 3536.83264235],
           [7260.9522096 ,    0.        , 9543.74292632],
           [3536.83264235, 9543.74292632,    0.        ]])
    
