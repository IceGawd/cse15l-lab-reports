# Part 1
## Code
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
	// The one bit of state on the server: a number that will be manipulated by
	// various requests.

	String keepingTrackOf = "";

	public String handleRequest(URI url) {
		if (url.getPath().equals("/add-message")) {
			String[] parameters = url.getQuery().split("=");
			if (parameters[0].equals("s")) {
				keepingTrackOf += "\n" + parameters[1];
			}
			else {
				return String.format("Need query 's'");
			}
		}
		String[] kto = keepingTrackOf.split("\n");	
		String toShow = "";
		for (int x = 1; x < kto.length; x++) {
			toShow += Integer.toString(x) + ". " + kto[x] + "\n";
		}
		return String.format(toShow);		
	}
}

class StringServer {
	public static void main(String[] args) throws IOException {
		if(args.length == 0){
			System.out.println("Missing port number! Try any number between 1024 to 49151");
			return;
		}

		int port = Integer.parseInt(args[0]);

		Server.start(port, new Handler());
	}
}
```
## Screenshots
![Image](add1.png)
![Image](add2.png)

# Part 2
![Image](l2p2s1.png)
![Image](l2p2s2.png)
![Image](passwordlessssh.png)
