# Download Html Source From Link

```
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp1
{
    internal class Program
    {
        private static List<string> allLinks = new List<string> {
            "https://www.farorecruitment.com.vn/the-amount-employees-can-receive-when-terminating-their-labor-contract-t_1/6272         ".Trim(),
            "https://www.farorecruitment.com.vn/tang-luong-co-so-tu-ngay-1-7-2023-ai-la-nguoi-bi-anh-huong--t_1/6236?lang=vi            ".Trim(),
            "https://www.farorecruitment.com.vn/increasing-common-minimum-salary-rate-from-1-july-2023-who-will-be-affected--t_1/6237   ".Trim(),
            "https://www.farorecruitment.com.vn/job-i2/1/2023/0/0/0/0/                                                                  ".Trim(),
            "https://www.farorecruitment.com.vn/                                                                                        ".Trim(),
            "https://www.farorecruitment.com.vn/Account/Login                                                                           ".Trim(),
            "https://www.farorecruitment.com.vn/Admin/Login                                                                             ".Trim(),
            "https://www.farorecruitment.com.vn/Admin/Dashboard                                                                         ".Trim(),
            "https://www.farorecruitment.com.vn/Admin/Account/ChangePassword                                                            ".Trim(),
            "https://www.farorecruitment.com.vn/Admin/Logout                                                                            ".Trim(),
            "https://www.farorecruitment.com.vn/Candidate/Login                                                                         ".Trim(),
            "https://www.farorecruitment.com.vn/Candidate/Dashboard                                                                     ".Trim(),
            "https://www.farorecruitment.com.vn/Candidate/Profile/Details                                                               ".Trim(),
            "https://www.farorecruitment.com.vn/Candidate/Profile/ChangePassword/                                                       ".Trim(),
            "https://www.farorecruitment.com.vn/Candidate/Logout                                                                        ".Trim(),
            "https://www.farorecruitment.com.vn/Candidate/Job/Bookmark                                                                  ".Trim(),
            "https://www.farorecruitment.com.vn/Candidate/Job/ApplyJob                                                                  ".Trim(),
            "https://www.farorecruitment.com.vn/Account/Register                                                                        ".Trim(),
            "https://www.farorecruitment.com.vn/Account/Register/?lang=vi                                                               ".Trim(),
            "https://www.farorecruitment.com.vn/Account/Login                                                                           ".Trim(),
            "https://www.farorecruitment.com.vn/Account/ForgotPassword/?lang=vi                                                         ".Trim(),
            "https://www.farorecruitment.com.vn/Account/ResetPassword?userId={0}&code={1}                                               ".Trim(),
            "https://www.farorecruitment.com.vn/Account/Login                                                                           ".Trim(),
            "https://www.farorecruitment.com.vn/Account/Login?lang=vi                                                                   ".Trim(),
            "https://www.farorecruitment.com.vn/terms-conditions_t5?lang=vi                                                             ".Trim(),
            "https://www.farorecruitment.com.vn/terms-conditions_t5                                                                     ".Trim(),
            "https://www.farorecruitment.com.vn/privacy-policy_p5?lang=vi                                                               ".Trim(),
            "https://www.farorecruitment.com.vn/privacy-policy_p5                                                                       ".Trim(),
            "https://www.farorecruitment.com.vn/hotcandidates-h4?lang=vi                                                                ".Trim(),
            "https://www.farorecruitment.com.vn/dich-vu-tuyen-dung-t_3/392?lang=vi                                                      ".Trim(),
            "https://www.farorecruitment.com.vn/executive-search-and-selection-t_1/257                                                  ".Trim(),
            "https://www.farorecruitment.com.vn/search-news_i1/1/0/ab                                                                   ".Trim(),
            "https://www.farorecruitment.com.vn/hotcandidates-h4?lang=vi                                                                ".Trim(),
            "https://www.farorecruitment.com.vn/our-services_i3?lang=vi                                                                 ".Trim(),
            "https://www.farorecruitment.com.vn/our-services_i3                                                                         ".Trim(),
            "https://www.farorecruitment.com.vn/executive-search-and-selection-t_3/257                                                  ".Trim(),
            "https://www.farorecruitment.com.vn/staffing-solution-t_3/258                                                               ".Trim(),
            "https://www.farorecruitment.com.vn/payroll-administration-t_3/259                                                          ".Trim(),
            "https://www.farorecruitment.com.vn/human-resource-compliance-t_3/260                                                       ".Trim(),
            "https://www.farorecruitment.com.vn/our-services_i3?lang=vi                                                                 ".Trim(),
            "https://www.farorecruitment.com.vn/dich-vu-tu-van-t_3/391?lang=vi                                                          ".Trim(),
            "https://www.farorecruitment.com.vn/dich-vu-thue-ngoai-nhan-su-t_3/393?lang=vi                                              ".Trim(),
            "https://www.farorecruitment.com.vn/dich-vu-tuyen-dung-t_3/392?lang=vi                                                      ".Trim(),
            "https://www.farorecruitment.com.vn/dich-vu-quan-tri-tien-luong-t_3/394?lang=vi                                             ".Trim(),
            "https://www.farorecruitment.com.vn/hotjobs-h2?lang=vi                                                                      ".Trim(),
            "https://www.farorecruitment.com.vn/han1562-t_2/7030?lang=vi                                                                ".Trim(),
            "https://www.farorecruitment.com.vn/apply-job_a2/7030?lang=vi                                                               ".Trim(),
            "https://www.farorecruitment.com.vn/consultant-corporate-solutions-vietnam--t_2/7018?lang=vi                                ".Trim(),
            "https://www.farorecruitment.com.vn/jobs-i2?lang=vi                                                                         ".Trim(),
            "https://www.farorecruitment.com.vn/about-us_a5                                                                             ".Trim(),
            "https://www.farorecruitment.com.vn/about-us_a5?lang=vi                                                                     ".Trim(),
            "https://www.farorecruitment.com.vn/?lang=vi                                                                                ".Trim(),
            "https://www.farorecruitment.com.vn/                                                                                        ".Trim(),
            "https://www.farorecruitment.com.vn/list-news_i1                                                                            ".Trim(),
            "https://www.farorecruitment.com.vn/list-news_i1/?lang=vi                                                                   ".Trim(),
            "https://www.farorecruitment.com.vn/ban-tin-thang-6-2021-s_1/5958?lang=vi                                                   ".Trim(),
            "https://www.farorecruitment.com.vn/search-job-h2/1/2023/0?lang=vi                                                          ".Trim(),
        };

        private static void Main(string[] args)
        {
            MainAsync(args).GetAwaiter().GetResult();
        }

        private static void OpenAllLinks()
        {
            foreach (var link in allLinks)
            {
                Process.Start(@"C:\Program Files\Google\Chrome\Application\chrome.exe", link);
            }
        }

        private static void GetAllLinks()
        {
            List<string> allLines = new List<string>();
            string filePath = @"C:\Users\ADMIN\Desktop\Faro.txt";
            string[] lines = File.ReadAllLines(filePath, Encoding.UTF8);
            for (int i = 0; i < lines.Length; i++)
            {
                string line = lines[i];
                if (line.Contains("https://www.farorecruitment.com.vn"))
                {
                    allLines.Add(line);
                }
            }

            File.WriteAllLines("Output.txt", allLines, Encoding.UTF8);
            Process.Start(@"C:\Program Files\Notepad++\notepad++.exe", "Output.txt");
        }

        private static async Task MainAsync(string[] args)
        {
            //GetAllLinks();
            //OpenAllLinks();

            var stopwatch = new Stopwatch();
            stopwatch.Start();

            var realPath = string.Empty;
            var htmlSource = string.Empty;
            foreach (var link in allLinks)
            {
                try
                {
                    var tempUrl = link.Replace("://", "_")
                        .Replace("/", "_")
                        .Replace("?", "")
                        .Replace("&", "")
                        .Replace("=", "")
                        .Replace("html", "")
                        .Replace("htm", "");
                    realPath = $@"D:\Pages\Faro\{tempUrl}.html";
                    string realFolder = Path.GetDirectoryName(realPath);
                    if (!Directory.Exists(realFolder))
                    {
                        Directory.CreateDirectory(realFolder);
                    }

                    using (HttpClient client = new HttpClient())
                    {
                        using (HttpResponseMessage response = await client.GetAsync(link))
                        {
                            using (HttpContent content = response.Content)
                            {
                                htmlSource = await content.ReadAsStringAsync();
                                if (!string.IsNullOrWhiteSpace(htmlSource))
                                {
                                    File.WriteAllText(realPath, htmlSource, Encoding.UTF8);
                                }
                            }
                        }
                    }
                }
                catch (Exception ex)
                {
                    Debug.WriteLine(ex);
                    //throw;
                }
            }

            string folder = @"D:\Pages\Faro";
            List<string> files = (from x in new DirectoryInfo(folder).GetFiles("*.html", SearchOption.AllDirectories) select x.FullName).ToList();
            foreach (var filePath in files)
            {
                string allText = File.ReadAllText(filePath, Encoding.UTF8);
                string newAllText = allText
                    .Replace("src=\"/", "src=\"https://www.farorecruitment.com.vn/")
                    .Replace("href=\"/", "href=\"https://www.farorecruitment.com.vn/")
                    .Replace("https://www.farorecruitment.com.vn/https://www.farorecruitment.com.vn/", "https://www.farorecruitment.com.vn/");
                File.WriteAllText(filePath, newAllText, Encoding.UTF8);
                Process.Start(@"C:\Program Files\Google\Chrome\Application\chrome.exe", filePath);
            }

            stopwatch.Stop();
            Console.WriteLine("Elapsed: {0} ms", stopwatch.ElapsedMilliseconds);
            Console.Write("DONE. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```
