# NSMGOA5
There are three main folders in OpenFOAM Case Folder.
They are as follows :
1. 0 - stores the boundary conditions for the simulation
2. constant - stores the mesh and material properties
3. system - stores the settings for the solver like no of iterations, write interval, type of numerical scheme, relaxation factor etc.
Since the study involves multiple domains, there will be each folder representing each domain in all the three main folders. 
So, everything must be described for each doamin separately. 
Steps to follow :
1.  Change the name of the folders acocrding to the name described in the geometry in each main folder.
2.  Change the name of the boundaries, while defining the boundary conditions, according to the name decribed in the geometry.
3.  Go to the 0 folder and change the initial conditions and boundary conditions of each domain according to the requirement. For example, ambient temperature and flow velocity. 
4.  Go to the constant folder and change the thermophysical properties of each domain and region properties file according to your requirement. 
5.  Go to the system folder and change the additional functions to monitor various parameters according to your requirement. You can also change the controlDict file for changing write interval and no of steps, according to the requirement.
6.  Import the mesh by ideasUnvToFoam command.
    Command will be of the form : ideasUnvToFoam your_mesh_name.unv 
    NOTE: This command is valid when the mesh is in the case folder !!!! 
    If mesh is not in the case folder then you need to mention the address of the mesh file.  
    Then command will be of the form : ideasUnvToFoam ......./your_mesh_name.unv   
7.  After the mesh is imported, you may be required to use transformPoints command if your geometry's dimension and your required model's dimension are not in the same order.
    Command will be of the form :transformPoints -scale "(1e-2 1e-2 1e-2)" ( if your geometry's dimension is in m whereas the model's dimension is in cm)
8.  Since the study involves multiple domains, so, the whole single mesh requires to be split according to domains involved. 
    Command will be of the form :splitMeshRegions -cellZones -overwrite 
    NOTE: Some new patches will be introduced representing the interfaces between domains. So, make sure that each and every boundary condition is described for those interfaces.
9.  Now the mesh is ready and you can check the mesh quality by the checkMesh command.
    Command will be of the form : checkMesh
10. If the mesh quality is good, then you can start the simulation by the chtMultiRegionSimpleFoam command.
    Command will be of the form : chtMultiRegionSimpleFoam
