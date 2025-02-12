# rararar
1. 

# Kreta.Backend StudentRepo

	public async Task <int> GetNumberOfManAsync()
	{
	    return await _dbSet!.CountAsync(s => s.IsWoman == false);
	}

2.

# Kreta.Backend IStudentRepo

	Task<int> GetNumberOfManAsync();

3.
# Kreata.Backend Controllers/StudentControllers

	 [HttpGet("NumberOfMan")]
	
	 public async Task<IActionResult> GetNumberOfMan()
	 {
	     return Ok(await _studentRepo.GetNumberOfManAsync());
	 }

4.
# Kreata.Backend Controllers/IStudentHttpServices

	Task<int> GetNumberOfManAsync();

5.
# Kreta.Backend Controllers/StudentHttpsService

	 public async Task<int> GetNumberOfManAsync()
	 {
	     try
	     {
	         int numberOfMan = await _httpClient.GetFromJsonAsync<int>("/api/Student/NumberOfMan");
	         return numberOfMan;
	     }
	
	     catch (Exception e) { 
	         Console.Write(e.Message);
	     }
	     return -1;
	 }

6.
# Kreta.Desktop Viewmodels/Controlpanelviewmodel

	1.
		[ObservableProperty]
		private int _numberOfMan;
	
	2.
		private async Task UpdateViewAsync() 
		{
		NumberOfMan = await _studentHttpService.GetNumberOfManAsync();
		}
	
7.
# Kreta. Desktop Views/ControlpanelView

	<StackPanel Margin="2" Orientation="Horizontal">
	    <TextBlock Text="Férfiak száma: "/>
	    <TextBlock Text="{Binding NumberOfMan}"/>
	    <TextBlock Text=" Fő"/>
	
	</StackPanel>
