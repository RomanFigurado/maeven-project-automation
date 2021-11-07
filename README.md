# maeven-project-automation
import io.github.bonigarcia.wdm.WebDriverManager;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

import java.util.concurrent.Callable;

public class Roman_20212069{
    WebDriver driver;
    @BeforeClass()
    public void setup(){
        WebDriverManager.chromedriver().browserVersion("94.0.4606.81").setup();
        driver=new ChromeDriver();
    }

    @Test
    public void executeTestUsingXpath(){
        String givenUrl = "https://www.saucedemo.com/";
        driver.get(givenUrl);

        WebElement username=driver.findElement(By.xpath("//div[@class = \"form_group\"]/input[@data-test=\"username\"]"));
        username.sendKeys("standard_user");

        WebElement password=driver.findElement(By.xpath("//input[@data-test=\"password\"]"));
        password.sendKeys("secret_sauce");

        WebElement btnlogin = driver.findElement(By.xpath("//input[@data-test=\"login-button\"]"));
        btnlogin.click();

        givenUrl = "https://www.saucedemo.com/inventory.html";
        String currentUrl = driver.getCurrentUrl();
        currentUrl = driver.getCurrentUrl();

        System.out.println("Verify current url vs given url- inventory");
        Assert.assertEquals(currentUrl,givenUrl);

        WebElement item=driver.findElement(By.xpath("//div[@class=\"inventory_item_name\"]"));
        item.click();

        String itemName=driver.findElement(By.xpath("//div[text()=\"Sauce Labs Backpack\"]")).getText();
        String givenItemName="Sauce Labs Backpack";
        System.out.println("itemName vs givenItemName");
        Assert.assertEquals(itemName,givenItemName);

        String itemPrice=driver.findElement(By.xpath("//div[text()=\"29.99\"]")).getText();
        String givenItemPrice="$29.99";
        System.out.println("itemPrice vs givenItemPrice");
        Assert.assertEquals(itemPrice,givenItemPrice);

        WebElement addToCart=driver.findElement(By.xpath("//button[@data-test=\"add-to-cart-sauce-labs-backpack\"]"));
        addToCart.click();

        WebElement cart=driver.findElement(By.xpath("//a[@class=\"shopping_cart_link\"]"));
        cart.click();

        givenUrl = "https://www.saucedemo.com/cart.html";
        String currentUrl2 = driver.getCurrentUrl();
        currentUrl2 = driver.getCurrentUrl();
        System.out.println("Verify current url vs given url-cart");
        Assert.assertEquals(currentUrl2,givenUrl);

        WebElement itemNameCart=driver.findElement(By.xpath("//div[text()=\"Sauce Labs Backpack\"]"));
        Assert.assertTrue(itemNameCart.isDisplayed());
        System.out.println("itemNameCart vs givenItemNameCart");

        WebElement itemPriceCart=driver.findElement(By.xpath("//div[@class=\"inventory_item_price\"]"));
        Assert.assertTrue(itemPriceCart.isDisplayed());
        System.out.println("itemPriceCart vs givenItemPriceCart");

        WebElement remove=driver.findElement(By.id("remove-sauce-labs-backpack"));
        remove.click();

        Assert.assertFalse(driver.findElement(By.xpath("//div[@class=\"removed_cart_item\"]")).isDisplayed());

        WebElement continueShopping=driver.findElement(By.id("continue-shopping"));
        continueShopping.click();

        WebElement item1=driver.findElement(By.name("add-to-cart-sauce-labs-bike-light"));
        item1.click();

        WebElement item2=driver.findElement(By.name("add-to-cart-sauce-labs-fleece-jacket"));
        item2.click();

        WebElement cart1=driver.findElement(By.xpath("//a[@class=\"shopping_cart_link\"]"));
        cart1.click();

        WebElement checkOut=driver.findElement(By.name("checkout"));
        checkOut.click();

        WebElement fName=driver.findElement(By.name("firstName"));
        fName.sendKeys("Roman");

        WebElement lName=driver.findElement(By.name("lastName"));
        lName.sendKeys("Figurado");

        WebElement postalCode=driver.findElement(By.name("postalCode"));
        postalCode.sendKeys("41000");

        WebElement Continue=driver.findElement(By.name("continue"));
        Continue.click();

        String price01String = driver.findElement(By.xpath("//div[text()=\"9.99\"]")).getText().replace("$", "");
        String price02String = driver.findElement(By.xpath("//div[text()=\"49.99\"]")).getText().replace("$", "");

        Double price1 = Double.parseDouble(price01String);
        Double price2 = Double.parseDouble(price02String);

        Double total = price1 + price2;

        String ItemTotal = driver.findElement(By.xpath("//div[@class=\"summary_subtotal_label\"]")).getText().replace("$", "").replace("Item total: ","");
        Assert.assertEquals(total.toString(), ItemTotal);

        WebElement finish=driver.findElement(By.name("finish"));
        finish.click();

        Assert.assertTrue(driver.findElement(By.xpath("//h2[@class=\"complete-header\"]")).isDisplayed());

        givenUrl = "https://www.saucedemo.com/checkout-complete.html";
        driver.get(givenUrl);
        currentUrl = driver.getCurrentUrl();

        Assert.assertEquals(currentUrl,givenUrl);
        System.out.println("URL Verified");


    }
}

