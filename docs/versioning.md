# Versioning of BTAS Releases #

BTAS uses [semantic versioning](http://semver.org/spec/v2.0.0.html), loosely defined. Our version numbers are of the form

<div style="font-size:110%;text-align:center;font-weight:normal;">
<span style="color:red;">Redesign</span>.<span style="color:#336699;">Improvement</span>.<span style="color:green;">Patch</span>
</div>

with the following meaning:

* <span style="color:red;font-weight:normal;">Redesign</span> releases can break client code through redesigning existing features and introducing new features broadly affecting the library.

* <span style="color:#336699;font-weight:normal;">Improvement</span> releases introduce significant new features and may extend the current API (such as adding optional function arguments) but should not break client code.

* <span style="color:green;font-weight:normal;">Patch</span> releases focus on bug fixes and should not to break client code or change the library API in any way (unless the API
itself is the cause of a bug).

Because BTAS is non-commercial and a research project in its own right,
we intend to depart from semantic versioning by not treating any <span style="color:red">Redesign</span> release numbers as special. Redesign release number 0 does not necessarily mean "alpha" code nor does Redesign release 1 indicate a special, stable reference release of the library. Nor do Redesign releases have a prescribed size: they may include large and extensive changes or simply small but crucial changes that nevertheless break client code.


</br>

[[Back to Main|main]]
